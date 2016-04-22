+++
date = "2013-01-29T01:18:02-06:00"
description = "Fake legal threats for fun and profit!"
draft = false
tags = []
title = "Honor Among Thieves: The Tonymacx86 hypocrisy becomes a story"
topics = ['Rants & Raves']

+++

Well, that was unexpected.

The very last post here has garnered me a "DMCA takedown notice: from an unspecified "Tonymacx86 legal".

Why all the scare quotes, you ask? Because the message I received isn't worth the bytes used to compose it.

I'd assume receiving such a notice would be rather intimidating. But... well, let's just have a look shall we?

<pre>
    Subject: DMCA Take Down Notice  
    From: ModBot  
    To: tk@tkware.info  
    Cc: team@tonymacx86.com  

    (my name and address)

    Sir,

    You are in violation of DMCA by posting the source code to UniBeast which is
    copyrighted by tonymacx86 LLC and is documented on line 8 in the content in
    question. This content along with any modified versions of UniBeast must be
    immediately removed from your site and any other site or server that you
    have shared this content with.

    Failure to comply with this notice will require us to take further action.

    This communication and it's content is confidential. As such, this content
    may not be disclosed outside of this email or any future communications by
    either party.

    Sincerely,

    tonymacx86 LLC Legal
</pre>

Sounds pretty scary. And indeed, I just about shat a brick when this landed in
my inbox. However, on calming down and some futher thought, it seems the folks
behind "tonymacx86 LLC Legal" seem to be unclear on what a DMCA takedown notice
is and requires.

Perhaps they should get better lawyers.


## DMCA What?

The Digital Millennium Copyright Act is a law, passed by the 105th congress, which amends the US Code to set out further definitions and extensions of copyright, basically.

The "notice" up above is a weak attempt (much like their weak DRM scheme from last post) at the real thing. This message does not constitute a DMCA takedown, because it's missing literally every element necessary to be one.

A quick reading of the DMCA law itself, section 512, subsection 3, paragraph A, sets out these requirements.

To wit:

<pre>
    ELEMENTS OF NOTIFICATION-

    To be effective under this subsection, a notification of claimed
    infringement must be a written communication provided to the designated
    agent of a service provider that includes substantially the following:

    (i) A physical or electronic signature of a person authorized to act on
    behalf of the owner of an exclusive right that is allegedly infringed.

    (ii) Identification of the copyrighted work claimed to have been infringed,
    or, if multiple copyrighted works at a single online site are covered by a
    single notification, a representative list of such works at that site.

    (iii) Identification of the material that is claimed to be infringing or to
    be the subject of infringing activity and that is to be removed or access to
    which is to be disabled, and information reasonably sufficient to permit the
    service provider to locate the material.

    (iv) Information reasonably sufficient to permit the service provider to
    contact the complaining party, such as an address, telephone number, and, if
    available, an electronic mail address at which the complaining party may be
    contacted.

    (v) A statement that the complaining party has a good faith belief that use
    of the material in the manner complained of is not authorized by the
    copyright owner, its agent, or the law.

    (vi) A statement that the information in the notification is accurate, and
    under penalty of perjury, that the complaining party is authorized to act on
    behalf of the owner of an exclusive right that is allegedly infringed.
</pre>

## Failing 6 ways from Sunday
Looking at these 6 requirements, and comparing against the "notice" I received, let's go point by point:

>(i). A physical or electronic signature of a person authorized to act on behalf of the owner of an exclusive right that is allegedly infringed.</strong>

Nowhere to be found. There's a vague "tonymacx86 legal", but no real signature. Certainly nothing resembling a real name or any legitimate pointer at a real person. This is a hard requirement - you cannot send a DMCA anonymously or as your company name - a specific person must be identified.

>(ii). Identification of the copyrighted work claimed to have been infringed, or, if multiple copyrighted works at a single online site are covered by a single notification, a representative list of such works at that site.</strong>

They claim I'm infringing their copyright to the UniBeast source code. And they don't really say much more than that. Whether a software crack is copyrightable or not is something i'd love to see tested, though!

>(iii). Identification of the material that is claimed to be infringing or to be the subject of infringing activity and that is to be removed or access to which is to be disabled, and information reasonably sufficient to permit the service provider to locate the material.

Nope. The message refers to a "line 8", but doesn't give so much as a web link. Line 8 of what? Line 8 of my blog? Line 8 of my famous recipe for chocolate chip cookies? Line 8 of my telephone pool?  The message reads as "the content in question"; what content? Where?

I'm not being pedantic here - I know exactly what this is braying about, but in order to be a valid DMCA, he has to actually point at it.

Furthermore, notice the words "service provider". DMCA's are always sent to the host of the content, not the person responsible for
posting it in the first place. Now, I can guess why this was done: Were Tonymac to have sent this to my webhost at the time, and they
ignored what a real DMCA is and just jumped on it, I could file a counter notice, get my content put back up, and furthermore, get the real
name and address of Tonymac, enabling me to file a federal counterclaim for bad faith use of the DMCA.

I'm guessing he wouldn't want that.

>(iv). Information reasonably sufficient to permit the service provider to contact the complaining party, such as an address, telephone number, and, if available, an electronic mail address at which the complaining party may be contacted.

Not even close. No address, no phone number. All I get are two nebulous email addresses (on the from: and cc: lines) which, for all I know, go into a bit bucket somewhere.

Oddly enough, Tonymac's site, and the email, makes a number of references to a "tonymacx86 LLC". I thought I'd be proactive and get the necessary contact information from their whois. Let's see here:

<pre>
    $ whois tonymacx86.com

    Registered through: GoDaddy.com, LLC (http://www.godaddy.com)
       Domain Name: TONYMACX86.COM
          Created on: 12-Jan-10
          Expires on: 12-Jan-15
          Last Updated on: 23-Dec-12

       Registrant:
       Domains By Proxy, LLC
       DomainsByProxy.com
       14747 N Northsight Blvd Suite 111, PMB 309
       Scottsdale, Arizona 85260
       United States

       Administrative Contact:
          Private, Registration  TONYMACX86.COM@domainsbyproxy.com
          Domains By Proxy, LLC
          DomainsByProxy.com
          14747 N Northsight Blvd Suite 111, PMB 309
          Scottsdale, Arizona 85260
          United States
          (480) 624-2599      Fax -- (480) 624-2598
</pre>

Oh wow. Not even a legitimate phone number. They registered the domain through "DomainsByProxy", a privacy protection service which renders any random person unable to contact the party on the other side. Great for random people running websites, but of questionable use for a legitimate business. I doubt whether this "Tonymacx86 LLC" actually exists. Let alone whether it has a "legal department".

>(v). A statement that the complaining party has a good faith belief that use of the material in the manner complained of is not authorized by the copyright owner, its agent, or the law.</strong>

No such statement in the email. This is **basic** boilerplate that any real DMCA will contain. This only further confirms my suspicion that this email was created by some random, not by a legitimate legal team.

>(vi). A statement that the information in the notification is accurate, and under penalty of perjury, that the complaining party is authorized to act on behalf of the owner of an exclusive right that is allegedly infringed.

Again, no such statement.

## Conclusion

Congratulations, "tonymacx86 LLC Legal"! Out of the 6 elements required to make a DMCA notice, you successfully completed zero of them.

<a href="http://tkware.info/wp-content/uploads/2014/11/Epic-fail-guy-dance.gif"><img class="alignnone size-full wp-image-26" src="http://tkware.info/wp-content/uploads/2014/11/Epic-fail-guy-dance.gif" alt="Epic Fail Guy Dance" width="400" height="400" /></a>

Speaking of confirming suspicions, this should raise further question in your mind if you plan on using any Tonymacx86 tools for your Hackintosh needs. Why would a legitimate organization/person/group/thing take the extraordinary step of trying to intimidate random bloggers with fake legal notices?

Should any "tonymacx86 Legal" people be reading this, consider this your notification that any further communiqué with me will be published, critiqued, and quite possibly mocked on this website. Your "confidentiality notice" is about as worthless as your "DMCA".

Furthermore, should they actually decide to pull their heads out and build a passable DMCA notice, it will also be submitted to the <a href="http://www.chillingeffects.org/">Chilling Effects clearinghouse</a> for public scrutiny and comment.

I sincerely doubt this will ever happen. Some further communications with others reveal that this is a pattern of behavior by the bullies at Tonymacx86,
but they never back up their big words with actions.
