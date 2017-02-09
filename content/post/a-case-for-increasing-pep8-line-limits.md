+++
date = "2016-05-08T14:22:46-06:00"
description = "Is 79 characters per line really enough in 2016?"
draft = false
tags = ['python']
title = "A case for increasing pep8 line limits"
topics = ['Tech', 'Rants & Raves']

+++

After some work on
[a recent project](https://docker.io/karunamon/concourse-resource-bitbucket),
I started tripping over
[PEP8](https://www.python.org/dev/peps/pep-0008/#maximum-line-length) (which is
the Python style guide of reference, used by most everyone and their tools),
specifically the requirement to use no more than 79 characters in a single line.

A read of these requirements sounds mostly sane. The idea being twofold, that:

* Extremely long lines mean that you're probably trying to cram too much functionality into a line, and should refactor your code
* It's easier for people to read lots of content vertically than it is to read horizontally

So far, so good.

It's much easier to make sense of this long function call:

```python
r = requests.post(
    post_url,
    auth=HTTPBasicAuth(username, password),
    verify=verify_ssl,
    json=js)
```

Than this one:

```python
r = requests.post(post_url,auth=HTTPBasicAuth(username, password),verify=verify_ssl,json=js)
```
However, where I start running into problems and annoyance is
when dealing with long strings.

## A stringly-typed error

Consider the following line of code:

```python
err("HTTP 403 Forbidden - Does your bitbucket user have rights to the repo?\n")
```

As written, this string is under the line limit. Ah, but remember, Python uses
indentation as a method of grouping code together. Say you wanted to run the
above bit of code inside a block that outputs the message if you run into an
error condition?

Your code then looks like:

```python
if error:
    err("HTTP 403 Forbidden - Does your bitbucket user have rights to the repo?\n")
```

Guess what? Your line is now 5 characters too long, and will be flagged by most
automated analysis tools.

The PEP8 solution for this is, to put it mildly, brain dead. In order to get the
above line of code under 79 characters, I'd need to do one of the following:


## Poor solutions to poor problems

Python has a (nifty?) little trick: implicit string concatenation.

This solution is non-optimal because it violates one of Python's main design tenets,
laid out in [PEP20](https://www.python.org/dev/peps/pep-0020/), the "Zen of Python",
namely "explicit is better than implicit"

Python, if it is given two strings separated by nothing but spaces, will silently
concatenate the two strings.

```
"foo" "bar" => "foobar"
```

If you surround the strings in parenthesis, you can add newlines:

```
("foo"
"bar") => "foobar"
```

This later one is a bit dangerous, since the only thing separating this string
concatenation from a tuple (a different object entirely) is a comma after the
first string.

```
("foo",
"bar") => ("foo", "bar")
```

..an all too easy mistake for someone reading your code to make.

To make it a bit more explicit, you can add a `str` in front of the paren.

However, syntax ambiguity and forcing reliance on magic implicit behavior isn't
the only problem here.

## Isn't readability the goal?

Let's go back to the long string of code we started looking at before:

```python
err("HTTP 403 Forbidden - Does your bitbucket user have rights to the repo?\n")
```

What's the right way to fix this? We have to somehow stick the two strings together,
and both ways actually make our code *less* obvious and *less* readable.

```python
err("HTTP 403 Forbidden -"
" Does your bitbucket user have rights to the repo?\n")
#or
err("HTTP 403 Forbidden"
" - "
"Does your bitbucket user have rights to the repo?\n")
```

Here we've added two lines of code for *very* marginal benefit, if not negative.

But this is just English. We can split up our broken human language any way we
want. Let's try something a bit more computer friendly, like a URL:

```python
build_url = "{url}/pipelines/{pipeline}/jobs/{jobname}/builds/{buildname}".format(
    url=os.environ['ATC_EXTERNAL_URL'],
    pipeline=os.environ['BUILD_PIPELINE_NAME'],
    jobname=os.environ['BUILD_JOB_NAME'],
    buildname=os.environ['BUILD_NAME'],
)
```

You already see some sane line breaks added. I broke up the keyword arguments to
format, placing each on their own line.

But what of our long URL string? Any possible way I can see of splitting this
line is going to make it more confusing to understand what's happening.

I could probably get away with using the old (deprecated) % operator on a string...


```python
build_url = "%s/pipelines/%s/jobs/%s/builds/%s" % (
    url=os.environ['ATC_EXTERNAL_URL'],
    pipeline=os.environ['BUILD_PIPELINE_NAME'],
    jobname=os.environ['BUILD_JOB_NAME'],
    buildname=os.environ['BUILD_NAME'],
    )
```

Icky. This carries the negative of making all of those 4 parameters positional,
and less readable still.

Discussing PEP8 online is usually a losing proposition as well...

## Response: Then just ignore them!

What's the purpose of having a standard if its application results in less readable code,
and reliance on implicit (i.e. "magic" and unintuitive) behavior?

Let's just get this out of the way: Any standard whose application has net negative
benefit when applied in the real world, and one to which criticisms are shamelessly
deflected with "you can just ignore that part" is a standard that both lacks value,
and is in need of updating.

Adding even 20 characters (actually 21, since we're at 79 now) would make this
problem mostly disappear, with minimal impact on readability.

PEP8 is usually (enforced/suggested) by automatic code analysis tools- those
can and should be configured to ignore PEP8 warnings when dealing with long strings, rather
than actual statements per line.

## TL;DR conclusion

* PEP8's line limit is an archaic albatross around the developer's neck.
* Most people are not coding on VT220s with an 80 character hard limit
* ...or on screens with a resolution smaller than 1920 pixels wide.
* Application of the limit reduces readability...
* ...and increases amount of code (and possibility for bugs by extension)
* Fixing this problem, either by adding an additional 21 characters, or adding an exception for strings, would not have a great negative impact on readability or developer usability
* Let's push past the impedance, ignore those who brush off all criticism of the standard,
* **and improve our fucking tooling already.**
