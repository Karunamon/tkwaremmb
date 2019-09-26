---
date: 2013-01-29T13:01:00-06:00
description: People who did nothing wrong don't rapidly change their behavior when caught
draft: false
url: 2013/01/29/unibeast-1-7-0-released-today-same-drm-shenanigans-and-hypocrisy-apply
tags:
- censorship
title: UniBeast 1.7.0 Released Today, Same DRM Shenanigans and Hypocrisy Apply
topics:
- Rants&Raves
- Your Rights Online
---

One day after my last post, talking about how silly the Tonymacx86 attempts at “antipiracy” are (considering that their tools amount to nothing greater than a software crack themselves), version 1.7.0 has been released.

Among the change notes is this:

* Removed misleading messages

No way!

So I downloaded the latest version and extracted it as usual. To my utter surprise, the `preinstall` script inside `extra.pkg` is removed outright!

Well then. So either they’ve gained principles and removed the check, or it’s been hidden elsewhere.

```shell
Skaia:~ tk$ mv UniBeast\ -\ Mountain\ Lion\ 1.7.0.pkg Unibeast170.pkg

Skaia:~ tk$ pkgutil --expand Unibeast170.pkg UniBeast170/

Skaia:~ tk$ grep -R piracy Unibeast170/.*
./Distribution:\b \cf0 Sharing or distributing the produced USB drive or it's contents is piracy and not condoned by tonymacx86 LLC
./dsmos.pkg/Scripts/preinstall:# Sharing or distributing the produced USB drive is piracy and not condoned by tonymacx86 LLC.
```

Oh. Apparently I ask too much; they just moved it around.

..into a package called “dsmos”.

Now that’s *very* interesting. **DSMOS** in any other context would refer to a Mac OS kernel extension. It stands for “Don’t Steal Mac OS X”. This module uses the hardware SMC present on real macs to prevent the OS from booting on any device other than Apple hardware.

I say this is interesting, because **this DSMOS kernel module is patched by Unibeast to allow Mac OS X to boot!**

There’s that honor among thieves, again. Disregarding and cracking one part of Apple’s rights while going out of their way to uphold the other.

What the f\*ck.

So let’s see what they’re checking this time. Inside Unibeast.pkg/dsmos.pkg/Scripts/preinstall:

* Lines 10-15: Check that the volume mounted isn’t called “Mac OS X Install ESD”

* Lines 17-22: Check for the existence of `_MASReceipt/reciept` in the install app

* Lines 24-29: Performs a `md5sum`(!!) of the receipt file to ensure it matches `f4747dbc07df72ad92a84186e2b5488d`

* Lines 31-36: Checks to see if the receipt file is less than 4600 bytes

* Lines 38-43: Checks to see if the phrase `com.apple.InstallAssistant.MountainLion` is not in the reciept (??)

They’ve definitely scaled up a bit, adding two more checks. Much to their credit, they no longer assert that a missing receipt is an indication of piracy. Now, if they’d remove these boneheaded checks outright, we could get back to every person being able to run whatever code they want on their own computer. But, barring that, we have to fix it ourselves..

The fix for 1.7.0 is identical to the fix for the earlier version, save we change a path and a digit:

```shell
pkgutil --expand "UniBeast\ -\ Mountain\ Lion\ 1.7.0.pkg" Unibeast-tmp && sed -e 8,47d -i bak Unibeast-tmp/dsmos.pkg/Scripts/preinstall && pkgutil --flatten Unibeast-tmp Unibeast-170-fixed.pkg
```

~~If this is problematic for you, I’ve also created an Automator app which will make the same change: Unibeast1.7.0-Patcher-V2.zip~~

**Edit: Nope. Just use the command line above (thanks John!). You should probably be familiar with the command line before making a modification like this anyways, and if not, you’re going to have a bad time hackintoshing ;)**

**Further Edit: The command above will only work on a Mac. It’s assumed that you have one since you’re using Unibeast, but if you unpackage the .pkg some other way on Linux, the sed command changes as follows:**

```shell
sed -i -e '8,47d' Unibeast170/dsmos.pkg/Scripts/preinstall
```

You’ll lose the cute googly eyes on the installer, but alas, such is the price of freedom :)

{{<figure src="/img/yodawgcracks.jpg">}}
