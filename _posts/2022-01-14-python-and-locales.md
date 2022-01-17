---
title: "🐍 Python and Locales"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - python
---

Beware when working with locales! So this post is kinda short and maybe a bit incoherent, but today I had a
facepalm moment at work that I want to preserve for a little while. 

# 🐍 Python and Locales

Back when you learned Python, you probably read that the code is platform-independent. You write your code, and if it works on your machine, it is expected to work on any other machine that has the same libraries installed.

Okay, once you deal with things close to the OS, such as filesystems, signals, et cetera, then it's reasonable to expect you code to not work anymore. I get that. But when you're dealing with highly non-OS-related stuff like localization, you shouldn't need to worry, right?

Riiight? 🤔 Hmmm...

Well, it turns out that things like locale-dependent sorting are also platform-dependent, if you trust your OS. This became apparent when I tried to access the REST interface offered by the BOC Group to do some business stuff. Auth worked fine on Windows, but as soon as I pushed the code to our Linux machines, it didn't. I got a 401, but only for cases where I passed some parameters. So I took a long and hard look at the [documentation](https://developer.boc-group.com/adoxx/en/token-based-authentication) in which you find the following paragraph:

  > Get the secret key matching to the identifier sent via the x-axw-rest-identifier header.
  > 
  > Take all request parameter names and put them into a collection.
  > 
  > (...)
  >
  > Sort this collection using Locale en_US.

Aha! Sorting using a specific locale... We got some locale issues earlier on, so I investigated and found a line like this in our implementation:
  
  > collection.sort(key=locale.strxfrm)

Some debugging then confirmed my suspicion: Locale-specific sorting using the `locale` module is platform-dependent! I repeat...
  
<image src=https://media.giphy.com/media/l2Jefdsvp5RAePehy/giphy.gif> 
  
**Locale-specific sorting using the `locale` module is platform-dependent!**
 
 
How the hells is something as abstract as this platform-dependent!? Well, whoever made this design decision surely had their reasons - I don't blame them. I was just highly surprised. Also, my gut told me I'm not the first to encounter this, since we aren't that special - despite nearly every organization believing this of itself. So I did a quick search and found [this issue which is in status "open" since 2015 (!)](https://bugs.python.org/issue23195#msg233691). The most recent comment goes like this:
  
  > In my experience, the locale module is error-prone and not reliable, especially if you want portability. It just uses functions provided by the OS. And the locales (LC_CTYPE, LC_MESSAGE, etc.) are process-wide which become a major issue if you want to serve different clients using different locales... Windows supports a different locale per thread if I remember correctly. It would be more reliable to use a good library like ICU.
  
Well, usually I hesitate to include a new third-party lib. But in this case I guess I'll make an exception.
  
 
