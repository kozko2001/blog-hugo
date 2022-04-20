
---
title: Export google authenticator to KeepassXC
date: 2022-09-25 00:00:00
---
---

1. Export from google authenticator an account you want (you should have now a QR Code)
2. convert the QR code to a link, I used qr journal.
	1. `brew install qr-journal`
	2.   Once done we should have an url with an schema that starts by `otpauth-migration://`...
3. Migrate to normal OTP code, luckily there is this project https://github.com/dim13/otpauth
	1. `go get github.com/dim13/otpauth`
	2. `~/go/bin/otpauth -link "otpauth-migration://....`
	3. Now we should have another url with a query parameter secret=......
4. We can go to Keepass, select our password entry, right click and setup the TOTP with the secret!

 