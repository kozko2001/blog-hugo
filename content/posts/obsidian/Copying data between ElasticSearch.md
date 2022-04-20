
---
title: ElasticSearch Dump
date: 2020-09-21 00:00:00
---
---
	
We are working in a migration from one ES to another, and for doing test is good to have some data from our staging environment.

one way is to use elasticsearch-dump, which basically allow you to get all the data from elasticsearch and dump it or send it to another elasticsearch server! 

```
npm install -g elasticsearch-dump
```

but with `elasticsearch-dump` you need to know what you want to dump... and who has the time to look around... but it turnsout this package has another binary that dumps everything, into a folder.

```
mkdir /tmp/es_dump;
multielasticdump --direction=dump --match='^.*$' --input=http://localhost:9200 --output=/tmp/es_dump

```

voila! 👑

and now, we just load the data into a the other elasticseach!

```
multielasticdump --direction=load --match='^.*$' --output=http://localhost:19200 --input=/tmp/es_dump
```


```
export INDEX=webshop_v5_20200909_110752_en
export OLD=http://localhost:9200/$INDEX
export NEW=http://localhost:19200/$INDEX

elasticdump --input=$OLD --output=$NEW --type=data --debug --limit=1000

elasticdump --input=$OLD --output=$NEW --type=mapping  --debug --limit=1000

elasticdump \
  --input=$OLD \
  --output=$NEW \
  --type=alias
  
elasticdump \
  --input=$OLD \
  --output=$NEW \
  --type=template
  
echo dump done!


```