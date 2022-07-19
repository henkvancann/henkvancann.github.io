---
layout: post
title:  "CESR, one of Sam Smith’s inventions, is as controversial as it is genius"
date:   2021-11-08 12:00
categories: identifiers
---
> medium-to-markdown@0.0.3 convert
> node index.js

[![Henk van Cann](https://miro.medium.com/fit/c/96/96/1*lHEKsx9xfeUiXPW2pqwC1Q.jpeg)

](https://medium.com/@hvancann?source=post_page-----d757f36b88f8--------------------------------)[Henk van Cann](https://medium.com/@hvancann?source=post_page-----d757f36b88f8--------------------------------)Follow

Nov 8, 2021

·7 min read

# CESR, one of Sam Smith’s inventions, is as controversial as it is genius. 

What is it, and why another standard? Why won’t this obstinate KERI project get out of the way and let us use an existing operational standard, for once?
===================================================================================================================================================================================================================================

**The main takeaway from this article is a kind of work assignment (“Me?!?” ‘Yeah, you!’): I’d like you to try and match the unique features of CESR to situations you might recognise as applicable.  
First, become an expert with this seven-minute-read article ;)**

![Obstinate or self confident?](https://miro.medium.com/max/1400/1*szgCSaRapKt1vdh45-sPiQ.jpeg)Obstinate or self sufficient? === Source Wikimedia Commons — Attribution 2.0 Generic (CC BY 2.0)

You can find documentation about CESR here: [https://github.com/WebOfTrust/ietf-cesr](https://github.com/WebOfTrust/ietf-cesr)

KERI resouces: [https://keri.one](https://keri.one)

Is CESR better, faster, safer? Most probably. But better then what? If you only tailor your goal to a small field of application, you can easily find your way to paradise.  
It’s always easy to be better, faster, safer in a subdomain that you’ve isolated from all the rest. A more generic IT standard has the undignified task of serving many masters. A dedicated standard is easier to achieve with the same effort.

Perhaps surprisingly, this obvious rationale was not the reason behind how and why CESR came to be. But we’ll get to the effect on our open source community of how and why CESR came about in a few minutes. Let’s kick off with one of the most pressing questions …

CESR — what is it?
------------------

The acronym stands for _Composable Event Streaming Representation._ But that says very little to the layperson. Let’s take that acronym apart.

**Composabillity**: lossless composition via concatenation. Hmm…, this explanation doesn’t really help, does it? Maybe an analogy might work. Suppose you were bored sitting in jail and wanted to use Google Translate to translate a piece of text from English to Dutch. Subsequently, as a way of killing your time, you keep copy pasting the resulting “to:” text into the “from:” field.  
Try it, and see what happens! Surprised? _The message changes until it comes to a standstill where you can keep swapping the texts without them changing._  
Before you get too happy about this result and dance the Jailhouse Rock with me, the sobering conclusion is: Google Translate is not composable!

By contrast, CESR is composable. The analogy lies in the fact that we consider two languages. Suppose the English in the Google Translate example is **readable, text based** in CESR and Dutch is the **binary** form in CESR. Within these two CESR “languages”, text-based and binary, you can concatenate and swap freely as many times as you like — the data won’t change in between in their binary or text form no matter what content you express with them. Isn’t that a giant leap for mankind? Well, no, not as an isolated feature — but that’s a topic for later.

Conversely, Google Translate is not composable. It will alter the text in consecutive round-robin swaps and alter its meaning in the process. Often ending up in complete gibberish:

![](https://miro.medium.com/max/1400/1*0DlQpelftMBbyCmolgkaow.png)initial translation![](https://miro.medium.com/max/1400/1*WJe7BnEPl7aEvFu0bl9RIQ.png)swap![](https://miro.medium.com/max/1400/1*uPP9nB_VUZjDE660gyR7-Q.png)swap 2![](https://miro.medium.com/max/1400/1*8LfB1ucH5P1UAYV0QgD8ng.png)swap 3![](https://miro.medium.com/max/1400/1*kX26Pinh7hjrRMYoZ0HGbg.png)swap 4![](https://miro.medium.com/max/1400/1*BxFBLDuHTSegMrt-_b-ynw.png)swap 5![](https://miro.medium.com/max/1400/1*5iqq6WQC9aZvLX-pGGzPqA.png)swap 6, end result is gibberish (senseless), Google Translate keeps repeating swap 5 and 6

I hope in this analogy it’s clear that key event streaming dearly needs **lossless composition** when going back and forth with the ‘same’ data in text-based and binary data representation in a lossless way. Furthermore, this needs to have the ability to conglomerate the data in a flexible way… In CESR terms: composability.

**Event Streaming**: The sheer volume of cryptographic material, primarily signatures, in a streaming application demands a streamable protocol. In CESR we’re looking at key events. Why? Because we had to handle key event logs and primitives in KERI over the internet asynchronously (departure and arrival times and sequence of data is unsure). The requirements were so demanding that no existing exchange format could comply. So the KERI team weren’t being obstinate, they just humbly accepted their fate and cheerfully created what was needed.

**Representation**: tables of derivation codes that CESR uses as prefixes represent types, offsets, counters for the bare cryptographic material CESR holds.

> You might think “OK, that sounds like CBOR and Multicodec (and like what else?), which has been around for years and is multifunctional and versatile” and you might ask yourself, still a little bit irritated, “Why another standard?! Why not add CESR to an existing standard?!”

This retoric illustrates the controversial side of CESR, mentioned in the title of the article. The simple answer is that for KERI purposes the existing standards just won’t do. And because KERI needed something different, CESR emerged from KERI requirements that existing solutions couldn’t fulfil.  
So if controversy in CESR exists it’s only in the perception of people that haven’t been able to verify its unique necessity?

Now let me try and illustrate CESR’s beauty. You might then embrace another convertible text to binary streaming format. Cheer up, let’s go!

Oops, wait, I forgot: **CESR — what does it look like?**

The example is annotated with comments, spaces and line feeds for clarity.

```
\-FAB     # Trans Indexed Sig Groups counter code 1 following group  
E\_T2\_p83\_gRSuAYvGhqV3S0JzYEF2dIa-OCPLbIhBO7Y    # trans prefix of signer for sigs  
\-EAB0AAAAAAAAAAAAAAAAAAAAAAB    # sequence number of est event of signer's public keys for sigs  
EwmQtlcszNoEIDfqD-Zih3N6o5B3humRKvBBln2juTEM      # digest of est event of signer's public keys for sigs  
\-AAD     # Controller Indexed Sigs counter code 3 following sigs  
AA5267UlFg1jHee4Dauht77SzGl8WUC\_0oimYG5If3SdIOSzWM8Qs9SFajAilQcozXJVnbkY5stG\_K4NbKdNB4AQ         # sig 0  
ABBgeqntZW3Gu4HL0h3odYz6LaZ\_SMfmITL-Btoq\_7OZFe3L16jmOe49Ur108wH7mnBaq2E\_0U0N0c5vgrJtDpAQ    # sig 1  
ACTD7NDX93ZGTkZBBuSeSGsAQ7u0hngpNTZTK\_Um7rUZGnLRNJvo5oOnnC1J2iBQHuxoq8PyjdT3BHS2LiPrs2Cg  # sig 2
```

Source: [https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html](https://weboftrust.github.io/ietf-cesr/draft-ssmith-cesr.html)

You see?, boring as bat shit and clearly an ugly message from Nerddom. Just joking, of course. If you want to learn more about what you see here, go to [github WebofTrust](https://github.com/WebOfTrust/ietf-cesr).

Now let’s go for the _real beauty_, to be seen by mere mortal experts…

![](https://miro.medium.com/max/1400/1*9l9-4TEhLuP8lpwPY98NQA.jpeg)Digital event data streaming — CC0 1.0 Universal (CC0 1.0)  
Public Domain Dedication

CESR is digital data streaming that
===================================

1.  Can freely concatenate pieces of data

2\. Has a fixed streamlet size in both text and binary format

3\. Converts back and forth from text to binary without data loss and round robin

4\. Is able to express complex data structures

5\. Is extensible with derivation codes

6\. Is extremely compact

7\. Works asynchronously, e.g. collecting primitives, such as individual signatures of a Multisig from the web.

8\. Is ready for post-quantum cryptography

9\. Contributes to legally sound identifiers, because everything is “readable” in text format.

“CESR doesn’t provide post-quantum proofing. The hash does. CESR just makes it easier to process the crypto material. How you use crypto material is not up to CESR.”  
_Samual M. Smith_

This list of reinforcing features might make you think of new fields of application. That’s not entirely surprising and, to reiterate, that was my only goal with this article.  
Let me offer you a few applicable and hopefully inspiring facts to play around with in your head.

_Composability_ allows text domain streams of primitives or portions of streams (streamlets) to be converted as a whole to the binary domain and back again without loss.

Fully qualified KERI cryptographic primitives are composable via _concatenation_ in both the text (Base64) and binary domains.

CESR’s approach to filling its derivation-code tables is a _first needed, first served_ basis.

In addition CESR’s requirement that all cryptographic operations maintain at least 128 bits of cryptographic strength _precludes the entry of many weak cryptographic suites_ into the tables.

Who is CESR for?
----------------

For actors in the KERI protocol: key controllers, witnesses, and watchers can exchange key events asynchronously over the web in a compact way. Notwithstanding that CESR is tailor-made for KERI, the standard could be used elsewhere, for example HCF’s Microledger. But you can do better, come on :)

How to use CESR?
----------------

Derivation codes serve several purposes and provide several features. One main purpose is to allow compact encoding of cryptographic material in the text domain. What we mean by text domain is any representation that is restricted to printable/viewable ASCII text characters. CESR is always used in a certain context (it doesn’t transfer context by itself).

When to use CESR?
-----------------

The derivation code tables have been filled on a first needed, first served basis. Check whether they satisfy your needs, if not, propose ammendments.

Create new — or use existing — context in KERI and start exchanging key events and/or key logs.

**Learn and appreciate CESR more in** [**KID001 comment**](https://github.com/decentralized-identity/keri/blob/master/kids/kid0001Comment.md)**.**

The KERI team are open to other ideas and want you to have fun creating them. Please try and match the unique features of CESR to situations, that you might recognise as applicable.

Acknowledgements
----------------

*   Thanks to Sam M. Smith for checking and completing a draft version of the article.
*   Creative Commons licensed pictures
