+++
date = "2016-04-21T13:24:53-06:00"
description = "A tool for scoring your days"
draft = false
tags = []
title = "TKWare Self Assessment System"
topics = []

+++
TSAS is scoring method I devised to quantify the quality of a day in my life. The idea is, while filling out a journal, contemplate various bits of the day and assign a set of categories a score between 1 and 4. There are six categories, each named to fit a memorable acronym: **HALOES**, standing for Health, Energy, sLeep, Overall, Energy, Synch.

Think of the ratings as a sliding scale with the following words attached:
    1 - Awful
    2 - Bad
    3 - Good
    4 - Awesome

## Changelog
TSAS1.0 - Initial release. Acronym: OCEANZ, rating from 1 to 10, same concept and categories.  
TSAS1.1 - Acronym becomes HALOES, rating from 1 to 5 (1-10 is too granular)  
TSAS1.2 - Rating system now 1 to 4, removes the ability for a "middle" rating that tells nothing.

## But first, a disclaimer

Note that this system is for SELF-INTROSPECTION ONLY. It has zero (proven) medical or diagnostic value, and only exists to help spot trends and generally make life better. No claims are made other than you're putting numbers to concepts.


## The Categories

Each of the six TSAS categories represent a different facet of your day. Remember, these are mostly subjective. Try to stay away from "3" ratings if at all possible unless you really *truly* can't decide whether a stat was better or worse for that day.

### (H)ealth:

**Key Questions**: How healthy did you feel today? Were you kinda icky, or kinda awesome?  
**Note**: This is *health*, not energy (that comes later), so try to think of this in terms of the way your body is functioning.  

**Example "1"**: Laid up with a nasty cold, migraines, etc. 1 means you are barely functioning.  
**Example "4"**: No health problems of any kind - not even sniffles or headaches. 5 means you are in perfect health.  

### (A)ttitude:

**Key Questions**: What was your mood today? Your outlook on the world?  

**Example "1"**: Nihilism, anger, hatred, depression. The world can go fuck itself.  
**Example "4"**: Happiness, peace, joy, love. The world is an awesome place.  

### S(l)eep:

**Key Questions**: How many hours of actual sleep did you get last night? Use the actual number, and *only* count time spent *actually* sleeping.  
**Note**: This is the one exception to the 'rate 1 to 4' rule. Decimal numbers are fine.  


### (O)verall:

**Key Questions**: On a scale of 1 to 4, how was your day?  
**Note**: This is a purely subjective score and is completely independent of the other numbers. If you are trying to average them, you're doing it wrong.  

**Example "1"**: Lost my job, ran out of money, pet died, etc.  
**Example "4"**: Won the lottery, met my soulmate, got promoted, etc.  

### (E)nergy:

**Key Questions**: Did you feel as if you had the energy to accomplish all you set out to do today?  
**Note**: Try not to confuse this with 'attitude'. You can have a bad attitude for the day and still have plenty of energy (or vice versa)  

**Example "1"**: Getting out of bed is a chore, and that's not to mention all the housework I'm not gonna do.  
**Example "4"**: I'm running a mile a minute and loving every moment of it. It's like I'm on speed  


### (S)ynch:
This one's a bit tricky to describe - I call it synch between mind and body. Have you ever had one of those days where you can't think, you're tripping on your own feet, and it just seems as if your body doesn't want to cooperate? That's a low synch day. A high synch day is one where thoughts come easily and you can accomplish whatever you set your mind to with relative ease.

**Key Questions**: How well were mind and body in harmony?  

**Example "1"**: Tripping over my own two feet, can't think, things I'm usually good at are difficult today.  
**Example "4"**: Busting things out at work, thoughts come naturally, moving around is easy and natural.  

## The Goal

Do this every time you write in a daily journal, and include the scores somewhere in each entry. Write it in a standard format, like H:4 A:3 etc. Then, later, you can parse out that info into a graph, and perhaps figure out what happened during each day to cause the impact to your assessment. Being a bit of a geek, I've got a template set up to encode this info into a YAML blob in my personal writings.

    TSAS1.2:
      H: 4
      A: 2
      L: 7
      O: 3
      E: 3
      S: 4

Simple and easy. I hope this provides a good baseline for whatever quntified self system you may come up with :)
