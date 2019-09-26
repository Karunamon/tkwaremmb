---
date: 2014-11-19T14:25:26-06:00
description: A mafia shakedown, coming to a website near you
draft: false
tags:
- Security
- Scams
title: The Certificate Authority Racket
topics:
- Tech
---

With Google's move to begin interpreting SSL encryption as a factor that goes
into determining a site's rank, no doubt the webmasters of the world are beating
a path to the doors of the Certificate Authorities which provide the
sought-after bits of code that enable your browser to connect to a  site without
being snooped on by others, whether those be kiddies on the coffee shop wi-fi,
or the kiddies who happen to work for the federal government.

Sounds like a good thing, right? There's just one problem: **The entire
infrastructure is rotten to its core!**

## SSL PKI: A primer

The general principle is like so: You want to connect to a website securely, so
the website presents a *certificate* containing its host name and some other
cryptographic information.

Your browser reads the certificate, does a handshake with the server, and
*voila*: the connection is encrypted.

So far, so good. There's still a weakness we have to deal with though: What
stops a malicious person from sitting between you and the server, presenting a
certificate saying they actually are the people you're connecting to, and
forwarding on your traffic to the other side without you knowing? This is what's
known as a *man in the middle* attack.

The answer is "Not much"; this is why we have the concept of Certificate
Authorities (or **CA**'s') basically a "trusted" (more on those scare quotes in
a moment) third-party that checks to see if the guy you're connecting to really
is who he says is, and "signs" the certificate.

This signature is ostensibly hard to get for a scammer. That way, if you connect
to a website, and the certificate you get isn't signed by a "trusted"
third-party, your browser throws up all kinds of scary warnings saying "Hey,
wait a sec, this certificate isn't signed, it could be from literally anyone!"

That is the theory, and on paper, it's good. In reality, there are a number of
huge problems with this setup.

## Getting Certified to Certify

Becoming a certificate authority, an organization that can sign certificates, is
a process that involves some technical chops and a ton of money. The technical
chops, to set up the (fairly complicated) signing mechanism in a technically and
physically secure way, and the ton of money to pass the audit to [receive a
certification](http://www.webtrust.org/homepage-documents/item27839.aspx).

With the audit certification in hand, you can apply to the various browser and
operating system vendors to include your CA - meaning that the OS or browser
will trust anything you sign implicitly. (The browser makers won't even give you
the time of day without this certification.)

And here we run into another problem:

## Trusting the trusted third party

There are literally **a few hundred** CAs that your browser trusts.

Example: [Here's a list of what Mozilla packages with
Firefox.](https://www.mozilla.org/en-US/about/governance/policies/security-group/certs/included/)
Do you know these companies? The ones in Japan? Israel? India? They're all over
the world. Do you know them? What knowledge do you have of how they became CAs?
What about their practices? **In short, there are more certificate authorities
than you have the ability and time to personally vet.**

CAs include those in governments with less than stellar records when it comes
to privacy and coercion. For instance, you can live in any country in the world,
and if the United States were to coerce a CA to make a certificate for, say,
Facebook.com, the US government now has the ability to snoop on the traffic of
anybody that trusts that CA's certificates, *regardless of their location,*
which almost certainly includes **you personally.**

"But wait!" "I hear you say. Isn't the very expensive audit supposed to serve as
a marker that this CA has been vetted?"

## Outsourcing trust is a horrible idea

This supposedly through and comprehensive audit doesn't stop CAs from being
broken into and bad certificates issued. Entire CA companies, such as
[DigiNotar](https://threatpost.com/final-report-diginotar-hack-shows-total-compromise-ca-servers-103112/77170/),
have been broken into and hackers have issued their own certificates for very
popular websites. The exact thing the audit is supposed to make impossible!

Indeed, all the audit does is prove that:

1.  A company has a great deal of money to burn (tens of thousands of dollars)

2.  The arbitrary requirements of the audit process were met when the audit was
performed

I liken this to  what happens when the city health inspector comes to visit the
local greasy spoon. Everyone goes on a cleaning spree, tidying up, killing the
rodents, throwing all the rotten food away, and washing their hands.

The audit is not an ongoing process, (save for a semi-yearly re-certification)
and once the health insp- sorry, auditors have left, the CA has no reason to
continue abiding by those standards.

Now, in theory, a CA that's been hacked badly enough will be de-trusted by the
browsers and the operating systems, by way of removing their certificate from
the trusted list, but in practice, this is never done. To my knowledge, a CA has
never been decertified for mere incompetence.

Also, an audit only superficially covers negligence, but not coercion at all.

All of the $30K+ audits in the world don't stop the local goons from knocking on
your door, quasi-legal letter in hand, and demanding you sign a google.com
certificate for them.

Speaking of goons:

## The relationship between a certificate authority and their customers is like
## a mob protection racket

Let's say you own a business. You want to sell things. Everyone and their dog
has it drilled into their head to look for a lock (and more recently a green
bar) in the address bar before turning over any personal info.

So you go to a random security company and get your certificate. If you get the
green bar one, this costs you roughly 300 a year and some time doing paperwork.

So, a year passes. This certificate for some ungodly reason "expires". This
means you get to pay your ma- I mean company the same $300 again just to get the
*exact same certificate you already have*, just with an updated date field.
There is literally no other difference.

You'll get emails from your company around expiration time, each more
urgent-sounding than the last.

The tone is invariable "That's an awful nice website you have there, would be
shame if SOMETHING WERE TO HAPPEN TO IT". If you say "to hell with this" and
allow the cert to expire?

{{<figure
src="/img/panda-ssl-cert-chrome.jpg"
caption="You get scary warnings like this">}}

It's not like the connection is unencrypted or your identity changed, nope, just
this arbitrary number is date + 1 day.

Why is this necessary? **It isn't. Pure and simple.** You don't use new keys
when you renew a certificate, so there is no technical or practical reason for
this expiration date, other than to line the pockets of the CAs.

## Even the free certificate authorities are horrible

The go-to free CA as of writing this is Startcom. I'd link them here, but I
refuse to send them traffic. They will provide basic SSL certificates for single
websites, for free.

Sounds good, right? What's a mob protection racket if they don't get money?
Well, there's a catch. Many catches, actually.

First of all, the UI on this site is horrible and confusing.

Secondly, and more importantly, you are charged money for the privilege of
*revoking a certificate*. Let's say you mistype the URL when you're setting up
your certificate. You now have a certificate you can't use (since if the domain
name on the certificate doesn't match the site that's showing it, scary browser
warning time), and these wonderful people at Startcom charge you $25 for the
purpose of killing off the old certificate.

This fee applies even if you're not trying to delete a certificate because your
own error. Remember [Heartbleed](http://heartbleed.com)? The bug that
necessitated a lot of people get new certificates since the private keys were
compromised? Yup - \$25 per certificate.

Startcom to their customers: "Fuck you, pay me."

## You are charged a lot for what you get

The best certificate authorities s that are not run by complete jerks appear to
be resellers of the jerks. For instances, [Gandi](https://www.gandi.net/ssl) is
a reseller. The least amount you can expect to pay for a certificate to pass all
of these checks and not get a scary warning on a single domain name is about
$10. Note that this is for the top-level name only. If you want to encrypt
"yoursite.com", you have to buy another certificate to protect
"subdomain.yoursite.com", and so on for every other domain you own.

There is a way around this, called "wildcard certificates", which is simply a
certificate issued to "\*.yoursite.com". The catch is that these certificates
are *absurdly expensive"*. The cheapest I've ever seen a wildcard certificate go
for is roughly \$130 per year. There is literally no difference between a
wildcard certificate and a single domain certificate, beyond the name getting a "\*."
in the front.

Speaking of differences, the other thing to remember is that certificates are
*fungible*. There is no difference between each company's certificates, save for
the name of the company doing the signing!

**This means that the $200 certificate from VeriSign is functionally identical
**and provides the same security as the $9 certificate from Gandi.**

## There has to be a better way!

So what are we to do? Self signed certificates are insecure because they can be
created by anyone for any domain - but the solution we've settled on frankly
sucks.

 The certificate authority system lets exploitative companies have way, *way*
 too much power. In the post Snowden era, centralization combined with this
 amount of power is **unacceptable**.

A number of solutions have been proposed.

One method is allowing self signed certificates, but having a distributed
network check the information on those certificates. Let's say you self sign
your certificate, and then the first time someone hits your website, the
connection goes through without warnings (after all, the chances that someone is
doing a man-in-the-middle attack on you *right now* is quite low), and the
details of the certificate you hit get sent out into a peer-to-peer network.

Then, every time someone else hits the same site, they check the certificate
they got against the network. If it's the same, the certificate already out
there gets a little bit higher of a score. If they're different, your browser
knows something is up, and stops you, asking for instructions. This allows you
to make an informed decision on what you want to connect to, without giving
rotten companies money. Decentralization is the future.

## You ~~are~~ used to be stuck

Boycotting the entire certificate authority system is untenable right now. You
can't refuse to do business with them, because they still have all the power.
You must do business with them or else your website visitors (possibly
customers!) get warnings in their browser designed to scare them away. My
suggestion? Get the cheapest certificates you can find (remember, the \$200
certificate does nothing that the \$9 certificate doesn't), and do your research
on the company that issues them. This way, you have some level of knowledge as
to what you're pushing out there, and you contribute as little as possible to
this rotten game. Keep an eye out - smart people are working on solutions to
this problem.

**Update**

Since this article was posted, a new CA started, headed up by the likes of
Mozilla. It's called [Let's Encrypt](https://letsencrypt.org), it's fully
automated, and charges nothing for certificates and revocation. Now, they don't
provide wildcard certs, but since the issuance process is automated and
scriptable, this isn't really a huge problem.

I highly recommend you check them out, and flip the likes of VeriSign and
StartCom the bird they so richly deserve.
