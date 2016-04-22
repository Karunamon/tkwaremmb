+++
date = "2013-01-27T15:09:26-06:00"
description = "Or: Why do I keep getting UniBeast install failures?"
draft = false
tags = ['hackintosh', 'piracy']
title = "Hypocrisy, thy name is tonymacx86"
topics = ['Tech', 'Rants & Raves']

+++

So I've spent this past weekend in a kind of interesting
situation. I own two macs, you see. One at home (which is very much
dead, after a rollover accident which saw it chucked out the window, and
Apple wanted north of $1K to fix), and one at work.

Both of these
devices run Mountain Lion.

Well, since the dead mac is basically useless
to me, I want to take its copy of Mountain Lion and install it on my PC.


*Technically*, this is against Apple's EULA.  
*Realistically*, I don't put
too much stock in what a megacorp claims their rights are on something
that I own and purchased :)

So, I headed over to the bay and downloaded
a copy of the App Store Mountain Lion installer, with the intention on
using it with a Tonymacx86 tool called Unibeast to generate a flash
drive I can use to install the OS on my desktop.

Well, I go through the
process, and the installer quits, saying it encountered an error. I dig
through my system logs, and I see this gem:

{{<highlight bash>}}
Jan 26 21:16:12 Skaia.local installd[3712]: ./preinstall: Piracy attempt detected, no MAS receipt found, exiting
{{</highlight>}}


I originally thought this was a new Apple check, so I take that error
message verbatim to Google. Where I end up is the Tonymacx86 forums, and I see lots of people having install failures. Their response is one that's
obviously canned: "Your copy of 'Install Mac OS Mountain Lion.app' is
incomplete, redownload it from Apple".

*Interesting..* I think. *It
seems they're being terribly evasive about this.*

Well, the message is in our logs is named as coming from a script called preinstall, so let's
look at that.

I use pkgutil to unpack the .PKG installer, and then grep
for the text of the error:

```
$ pkgutil --expand Unibeast.pkg Unibeast-tmp
$ grep -iRo piracy Unibeast-tmp/
preinstall: piracy
```

Gotcha. Sure enough, in the preinstaller script, is this lovely bit of
weak-sauce DRM:

{{<highlight bash>}}
if hdiutil detach "/Volumes/Mac OS X Install ESD/" -force -quiet $2> /dev/null; then
  echo " "
  echo "Piracy attempt detected, exiting";
  echo " "
  exit 1
elif [ "$(file -b /Applications/Install OS X Mountain Lion.app/Contents/_MASReceipt/receipt)" != 'data' ];then
  echo " "
  echo "Piracy attempt detected, no MAS receipt found, exiting";
  echo " "
exit 1
  elif ! grep -q com.apple.InstallAssistant.MountainLion /Applications/Install OS X Mountain Lion.app/Contents/_MASReceipt/receipt ;then
  echo " "
  echo "Piracy attempt detected, invalid MAS receipt, exiting";
  echo " "
  exit 1
else
  cp /Applications/Install OS X Mountain Lion.app/Contents/_MASReceipt/receipt "${3}/.receipt"
fi
{{</highlight>}}

Crude DRM in a tool which exists only to help break Apple's DRM. WTF?

In any case:

## The Tonymacx86 project or any files or tools sourced from there can NO LONGER BE CONSIDERED TRUSTWORTHY.

Why? If they're willing to resort to tricks
such as this to waste your time, using a script that runs with elevated
permissions, it's a quite short jump from there to causing system
damage. 

Imagine instead of echoing something out to the syslog, they
threw an \`rm\` in there on something vital. A kext or two. Maybe
messing with other partitions on your disk. It doesn't take much to make a
system unbootable... I'll be staying far, far away from these losers in
the future.

Now, as an example of how utterly ineffective this kind of
"DRM" is (like most kinds of DRM actually), here's how you fix the bug
and get Unibeast to work regardless of the source of your Mountain Lion
installer. In one line of bash:

```
pkgutil --expand Unibeast.pkg Unibeast-tmp && sed -i 27d Unibeast-tmp/multi.pkg/Scripts/preinstall && pkgutil --flatten Unibeast-tmp Unibeast-fixed.pkg
```

We unpack, drop the first 27 lines of the preinstall script (which serve
no purpose whatsoever other than to inconvenience people), then repack. Now the original tool
is usable, and free of any timewasters installed by busybodies.

Still. This will get you through the install you're probably here to do, but in
the future, I'd suggest using something like MyHack. Tonymac is a proven buffoon
buffoon and cannot be trusted.

**Update**

And if that last line wasn't proven just from the existence of DRM in a DRM breaker,
check out the next article, where he sends me ineffectual legal threats!
