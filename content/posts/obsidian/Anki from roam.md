
---
title: Anki from Roam
date: 2020-07-19 00:00:00
---


DRAFT !





Goal: Able to extract the anki  flashcards from own notes


Definition of Success:
  - **Given** I do some changes in my roam files
  - **And** I add a new flashcard node
  - **When** some time happens (1h)
  - **Then** in my phone (ankiDroid) I have my new flashcard


Highlevel:
  - Download the markdowns
  - Parse all the markdowns and find the cards
  - Send the cards to anki somehow


Anki
  - highly personalizable software
  - LOT, lot, loooot of addons
  - makes it hard to understand how it actually works


Research, how I can update anki from my server
  - The oficial way to sync between different devices in anki is to use ankiweb, but ankiweb has no public api
  - AnkiDroid, the app for anki in android, has a Droid API => 💡 create an app that gets the data from an s3 bucket or a server. downloads it, and creates the deck
  - there is a ankysyncd and a docker container project (https://github.com/kuklinistvan/docker-anki-sync-server) which would be possible to modify to add the decks/flashcard in there..


First approach android app!


Project steps
  - Create a single app with a button
  - [x] When the button is pressed will create a new card in the test deck
      - Validation: if the card is also sync agains ankiweb, and appears in the anki desktop! => **Yes, if you click the sync button in the app, in settings there is an auto sync**
      - Validation: what happens if we try to create two equal cards => **Multiple cards are created**
  - [x] Will create a roam deck if it don't exist and will create the card
      - Validation 
  - [x]  Every hour will create the an anki flashcard with the time stamp
      - Validation: we can create cards from the background
  - [x] Define a valid json format  and create a simple test, that the app can download, and create the card
```clojure
{
  decks: [{
    name: "Roam",
    cards: [{
      type: 'cloze',
      text: 'which is the capital of Costa Rica San Jose'
    }, ...]
   }, ....]
}
```

  - [x] Define a valid json format  and create a simple test, that the app can download, and create the card
      - Had to do a lot of hacks, cause like the ankidroid api doesn't expose enough, it allow for creation, but note to get all the notes (only by id)

  - [ ] from roam to deck json file check for inspiration https://github.com/chronologos/roam-to-anki
  - 