---
layout: post
title: "Python history, a talk from Guido"
date: 2013-10-18 23:17
comments: true
categories: 
---

This [talk](http://bit.ly/nsaEak) titled "History of Python" is from Guido at Dropbox, before he joined Dropbox. It's a great talk, especially for python fans like me. 

# Notes

Guido was inspired by ABC. He commented on ABC's goods and bads.

Python is originally for day to day work (yes, every language inventor says that).

He had good summary on the philosophies behinds python, and they're also useful for other tasks.

    Skunkworks (early days) Design philosophy
    - Borrow ideas whenever it makes sense
    - As simple as possible, no simpler (Einstein)
    - Do one thing well (UNIX)
    - Don't fret about performance (fix it later)
    - Go with the flow (don't fight env)
    - Perfection is the enemy of the good
    - Cutting corners is okay (get back to it later)

    User-centric design philosophy
    - Avoid platform ties, but not religiously
    - Don't bother the user with details
    - Discourage but allow coding to the platform
    - Offer multiple levels of extensibility
    - Errors should not be fatal, if possible
    - Errors should never pass silently
    - Don't blame the user for bugs in python

Also, he recalled the process of python community growing up. That's the main reason of python's success.

In Q&A section,

- Didn't know unicode at early days
- About pyc files:
    - the first version of python doesn't have pyc, it parses the module first, but,
        - the parser is relatively slow
        - need much memory
    - some may release pyc file to avoid source code leak, but there're pasers can decode pyc well
    - python3 only have one directory for pyc files
- Regrets about python
    - lambda can be done in other ways
    - reduce() method is hard to read
    - unicode for python2
- Alternative python implementations
    - always encourage others
    - pypy is written by increadible smart peoples, sometimes they're too smart for their own good, they write really complicated stuff, ... some code has explosion of cleverness, you hope it's right, if not, there's only one person in the world can debug it
- Q: back to early days, will you do unit testing, what would it look like?
    - In 96-98, we made long effects to add tests, before that, very few tests
    - Not much sense about testing in early days
- Python2 and python3
    - In 5 years, everybody gonna use py3

# Others

I've seen Guido's talk several times, and luckily seen in person once. He's a typical geek to me, has his own style, talks slowly and logically, mature, respect the audiences, and love to interact with community. And he's  pratical, you can know that from this talk. He may not like to do "really" smart things to amaze the crowd.
