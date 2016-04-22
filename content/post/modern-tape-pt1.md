+++
date = "2015-10-04T11:43:26-06:00"
description = "Part 1"
draft = false
tags = []
title = "Modern Tape Backup - The Why"
topics = ['Tech', 'Enterprise']
series = "Modern Tape Backup"
+++

Ask a sysadmin nowadays about tape backup, and you'll get a lot of answers, most of them negative. Here are some choice quotes from a question (is tape backup viable nowadays?) floated to some friends and a few IRC channels:

<blockquote>Tape? Who uses that anymore?</blockquote>

<blockquote>Nah, way too expensive and hard to deal with. We backup to spinning disks.</blockquote>

<blockquote>In 2015? lol</blockquote>

Ouch, huh? It's no wonder people have such a negative opinion - tape is widely seen as an outmoded, unusable relic of a bygone era. Think "tape", and you think large reel-to-reels in IBM datacenters circa 1970. The mental image conjured is... unflattering.

I'm here to tell you that's **completely untrue**. Tape carries a number of benefits unmatched by any other storage medium.

Why should you care?

### Tape backup has the best gigabyte-to-dollar value available

Even an older generation tape technology, [LTO-4](https://en.wikipedia.org/wiki/Linear_Tape-Open#Generations), has a storage capacity of 800GB per tape (and possibly up to 1.5TB with hardware compression). Single brand new LTO4 tapes run about $25 each (with bulk discounts or careful shopping in some cases running that down as low as $15). Even if we assume **zero** compression capability (perhaps you're backing up a great deal of encrypted data?), that's an *upper limit* of $31.25 per terabyte, **or just a hair over 3 *cents* per gigabyte.**

Newer tech, LTO5, basically doubles the value. With an uncompressed capacity of 1.5TB, and with good compression, 3TB, and with the tapes around that same $25-each price, the cost falls even further, to a maximum of **just over a penny per gigabyte**.

Newer still, and the top of the line today, LTO6, with similar tape prices, are literally penny per gigabyte. ($25/tape, 2.5TB/tape)

You aren't going to find a better value in any other medium.

Oh, by the way, LTO7, the next generation, is due out some time in 2016, and is planned to hold 6 terabytes per tape, up to 15 terabytes compressed. If the same price point holds for the tapes, expect to see sub-penny per gigabyte costs.

LTO4 standalone drives can be had for the low hundreds, as can automated tape libraries.

### Tape backup has the best reliability available

The other big benefit tapes have going for them is its reliability. [A 2010 study commissioned by Oracle](http://www.oracle.com/us/corporate/analystreports/corporate/esg-nersc-case-study-202702.pdf) read back over 24 **thousand** tapes (some up to 12 years old). The result? 13 of those 24,000 tapes contained errors, and of those errors, most were single-block errors, meaning most of the tape was still readable.

### Tape backup is an enterprise standard

Tape may not be the latest and greatest, but it's Good Enough for enterprise usage. The same Oracle study from before showed roughly identical numbers for disk archival storage vs tape archival storage (only 5% more disk storage). And since it's enterprise standard, software and hardware to work with it is both plentiful, and in many cases, inexpensive. Interacting with tape units doesn't need an expensive license of [clunky software like Backup Exec](http://geekty.blogspot.com/2013/08/symantec-backup-exec-2012-sucks-backup.html) and accompanying Windows license - today, you can get the same reliability and full feature set from something like [Bareos](https://www.bareos.org/en/) as a completely free and open source product, with the [full paid support (PDF)](http://www.bareos.com/en/Pricing.html?file=files/pricelists/bareos-pricing.en.2015.03.pdf) if you feel you need it.

## The downside(s?)

Tape's one flaw, the one thing that gets brought up in most discussions, is its read/write speed. Yes, it's relatively slow. LTO6 technology has a max uncompressed write rate of 160MB/s, with similar read rates. But you need to ask yourself some questions before writing the medium off:

* This is for backup, right?
* This isn't for primary storage, right? I've got spinning disks for that.
* This is what I store my data on so I can recover it if something bad happens, right?
* Am I **generating** more than 100 megabytes per second of data?
 * If I am, is that a problem I could work around with additional drives?

That last thing bites many companies in the video on demand business. If that's your line of work, it's very likely that you are literally taking in more data every day than you can reasonably back up to offline storage. And with VoD, the content provider can resend you the content anyways. But - consider whether it would be worth having your other information backed up offline. Virtual machines, configuration files, and the lot.

Write speed *probably* isn't a problem that you will need to deal with in your line of business. Please, run the numbers yourself. You may be surprised!

In part two of this series, we will walk through setting up a Linux tape backup solution using some inexpensive software and hardware.
