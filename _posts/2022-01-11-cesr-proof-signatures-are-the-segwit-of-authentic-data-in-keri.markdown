---
layout: post
title:  "CESR Proof Signatures are the “Segwit” of Authentic Data in KERI"
date:   2021-01-11 12:00
categories: identifiers
---
# CESR Proof Signatures are the “Segwit” of Authentic Data in KERI.

Has the seemingly inevitable bolt-on party begun in KERI? Or is CESR Proof Signatures a structural innovation in the Verifiable Credential field?
> Completely new to KERI and CESR? Start [here](https://keri.one).

This article is about streaming signatures that authenticate data. However, it has a much broader context. *KERI* solves the secure attribution problem* of **“who said what?!”** on the internet with crypto-graphical derivations. V*erifiable credentials* (or attestations) solve the veracity problem with governance; **“is it true?!”**. 
The two aspects of trust, secure attribution and veracity, combine in CESR Proof Signatures. Is this combination new and unique? Is it a burden or a joy?

![Copyrights unknown, from [WWW.THEWRiTECONVERSATiON.COM](http://WWW.THEWRiTECONVERSATiON.COM)](https://cdn-images-1.medium.com/max/2140/1*lZpNgaMtg-ePnuN1hmRizA.jpeg)*Copyrights unknown, from [WWW.THEWRiTECONVERSATiON.COM](http://WWW.THEWRiTECONVERSATiON.COM)*

The only intention of this article is to make you never forget the connection between CESR Proof Signatures and the *image* of **scattered pieces of digital signatures confidently floating around in cyberspace.** “Confidently*”*, because these particles, once received and put back together as a whole, won’t have lost a bit of their integrity, their security or their effectiveness.

But enough of floating and imagining. Let’s get our feet back on the ground and start to answer some questions. Take off your headset, maximise this window, and chase away your colleagues or family members, because you’ll need your full focus for this.

*Secure attribution over the internet is difficult. Because, whatever someone says about the other end’s claims, you can always respond “Oh yeah, how can you be one hundred percent sure?!”. And they can’t.

![From [keri.one](http://keri.one)](https://cdn-images-1.medium.com/max/2908/1*Kax8Grdm26zYJl5Dl0Kvhg.png)*From [keri.one](http://keri.one)*

**How are KERI and CESR related?**

In [this article](https://medium.com/happy-blockchains/cesr-one-of-sam-smiths-inventions-is-as-controversial-as-genius-d757f36b88f8) I’ve tried to explain why KERI takes its own course with CESR. Headstrong as the team has been about an own version of an *event streaming* representation, we have just had to wait for a point in time when they have to start building bolt-ons? Is it the price to pay for stubbornness?

![Creative Commons license — Endless rabbit hole?](https://cdn-images-1.medium.com/max/2048/1*bwREG5iKIv6fV3dUB9Cgsg.jpeg)*Creative Commons license — Endless rabbit hole?*

To answer this question objectively we need to step to the side to look at some extra terminology not addressed in the article just mentioned. Repeat the terms aloud to remember the slight — but relevant — differences.

**Self-Certifying Identifier (SCI)**

In brief: A self-certifying identifier cryptographically binds an identifier to a key-pair.
It is an identifier that can be proven to be the one and only identifier tied to a public key using cryptography alone.

![From [keri.one](http://keri.one)](https://cdn-images-1.medium.com/max/4816/1*4oh1O7iV0R82AW9kqRuVzg.png)*From [keri.one](http://keri.one)*

**Autonomic Identifier (AID)
**An identifier that is self-certifying and self-sovereign. The former feature is defined above, the latter means leveraging a new model for Internet-scale digital identity based on an emerging set of protocols, cutting edge cryptography and open standards. Technological and social movements have come together to make self sovereignty possible ([Source](https://livebook.manning.com/book/self-sovereign-identity/chapter-1/v-8/14))). 
Decentralisation of the `root-of-trust` and `verifiable credentials` come into play and this mechanism delivers “*user-centric identity*”: more control and self-determination of individuals, machines and combinations of these, that identify as one.

**Key Event Log (KEL)**

This log consists of Hash-chained Key Events. These are blockchains, narrowly defined, but not in the sense of a global consensus mechanisms (not needed). Every KEL is ordered, but only in respect to the events about just *one* identifier. There is no global consensus mechanism because there is no need for total global ordering. So events in a KEL are ordered against themselves but not against events from any other KEL. AIDs have KELs, SAIDs don’t. Our AIDs KEL makes the control over these identifiers verifiable to the Root of Trust, we call this *end-verifiable*.

**Transaction Event Log (TEL)**

Externally anchored transactions via cryptographic commitments in a KEL. The anchor is also called a *seal*. The set of transactions that determine registry state form a log called a Transaction Event Log (TEL). The SADs mentioned above are registered here. The TEL provides a cryptographic proof of registry state by reference to the corresponding controlling KEL. Any validator may therefore cryptographically verify the authoritative state of the registry.

**Self-Addressing Identifier (SAID)**

Data may be directly embedded in a KEL or it may be anchored to a KEL using a cryptographic digest or SAID (self addressing identifier). A SAID is a self-referential digest as identifier. Given that the cryptographic strength is sufficient, any digest anchored data has the same verifiable security guarantees as the embedded data for which is was derived.

Otherwise defined: A self-addressing identifier (SAID) is a special class of *content-addressable identifiers* that is also self-referential. This means it is a self-certifying identifier (SCI) that has been attached to a certain context or infrastructure at the time of its inception. Any identifier which is deterministically generated out of the content, a digest of the content is a SAID.

**Self-Addressing Data (SAD)**

The pointer to digital data that can be derived from (a digest of) the data itself.
> Example: a table that contains a digest of the column 2 (a hash) in the index column 1, which in turn points to the data of that row in column 2.

A SAD (Self-Addressed Data) item is a serialization of a data item that includes its SAID. A commitment to the SAID of a SAD is cryptographically equivalent to a commitment to the SAD itself.

For self-addressing data, it is important to mention that the “pointer” (SAID) is also included as the identifier *in* the data itself. The [SAID specification](https://weboftrust.github.io/ietf-said/draft-ssmith-said.html) spells out the algorithm for generating the pointing SAID. 
Now first promise you won’t run away from this article, only then we (!) will tell you how it’s done. Plus why this is important. Promise?!

Here we go: Generating the pointer SAID is done by padding out the id field before creating the digest and then inserting the resulting SAID in the SAD. Creator of CESR Proof Signatures Phil Feairheller explains why it is done this way:
> “The SAID is generated this way to ensure that there is one and only one identifier for this content and that it is content addressable. With a standard digest approach, usually there is an identifier (like a URN or database ID) embedded in the content. Then the content has two identifiers and indexing them in something like a database and a content addressable hash can be problematic and lead to security issues. With our approach, the content addressable identifier and the identifier embedded in the content are one and the same. No confusion or opportunity for compromise.”

Great you’re still here, as promised. Admittedly, I had to read Phil’s stuff trice myself, before I could tell things apart again. Keep your head, you’re not alone.

**Map**

When creator Phil Feairheller uses “map” in the specification, he’s referring to a **hash map data structure** common in most programming languages that holds key-value pairs, and the data structure represented by the *many* type in CBOR, JSON and MessagePack. So its a map in Javascript, a dict in python and a HashMap in Java. The most important feature that's worth pointing out is that any *Map* type used **must remember original insertion order of the keys** to provide a consistent serialization so signatures can be verified against identical data.
**Not to be confused** with *maps* in the context of digital (multi) signature which are a *cryptographical function* that secures signatures against forgery.

You’re still with us? Exceptional. Let’s get into the finals.

**Transposable Signature Attachments (TSA)**

![](https://cdn-images-1.medium.com/max/3500/1*Ogryp389pp54vIE5Y8UEjQ.png)

There are several events in KERI that can contain context specific embedded self-addressing data (SADs). Exchange events (exn) for peer-to-peer communication and Replay events (rpy) for responding to data requests as well as Expose events (exp) for providing anchored data are all examples of KERI events that contain embedded SADs as part of their payload. If the SAD payload for one of these event types is signed with a CESR attachment, the resulting structure is not embeddable in one of the serializations of map or dictionary like data models. (JSON, CBOR, MessagePack) supported by CESR. **To solve this problem, CESR Proof Signatures are transposable across envelope boundaries** in that a single SAD signature or an entire signature group on any given SAD can be transposed to attach to the end of an enveloping SAD without losing its meaning.

And this is where the *stepping to the side* rather abruptly ends. Like a plot in a cult film. A quick reminder: we’re on our way to imprint the image of scattered pieces of digital signatures confidently floating around in cyberspace. And the mother ship has just been defined: Transposable Signature Attachments.

**Back to the Light**

![Back to the light](https://cdn-images-1.medium.com/max/2384/1*SLhKl9ARBDINlfjPtAvY1A.png)*Back to the light*

We seem to have gone down a rabbit hole, don’t we, that is collapsing in on us…? But the good thing about side steps is that you get knowledge you didn’t expect to get.
> # Why can’t I just answer the question and chose between ‘extension’ and ‘bolt-on’? What more do we need to know to be able to judge CESR Proof Signatures?

First we should understand that non-KERI SADs can be complex, nested beasts compared to native KERI SADs in TELs. And that means that all the nested pieces can have various protocols of multi-signatures attached to them. Just imagine a giant nested data structure virtually floating around in space and not being able to chop it into smaller pieces nor being able to encrypt / decrypt it from text to binary and vice versa…. Musician Damien Rice wrote how this might end:
> # “…it’s not hard to fall, when you float like a cannonball.”

Conversely, the design principles of ‘CESR Proof Signatures’ are:
- secure
- composable text — binary
- transposable signatures across envelope boundaries
- minimally sufficient means
- uniform and standardized
- parsable (a language)
- variable length

The last design principle requires us to get a better understanding of the relationship between the streaming format and the static field length required for signature maps. These two are conveniently matched for CESR Proof Signatures. Feairheller explains “CESR Proof Signatures are not fixed length, they are variable length, because the PATH element of the signature can be any length. That’s why we had to use the new variable length codes that Sam Smith added to CESR.”

Now that that’s done, we can move forward to the most important question…

### Why do we need an extension to CESR, at all?

![Creative Commons license — The big Why](https://cdn-images-1.medium.com/max/4000/1*QvmjDZ7FVGk2MmAnA8MK2Q.jpeg)*Creative Commons license — The big Why*

CESR Proof Signatures include non-KERI events (other SADs) that require signature attachments. This means KERI is inviting guests over and CESR will be their host.
> For example a complex real estate transaction document* from a notary that contains nested signatures** of selling heirs of an object can be used by the buyer as a virtual credential to opt for a mortgage. This event could cut back lead-time of a real estate transaction, because banks do not have to wait for the contract to be signed.
> * guest data must be self-addressing, a SAD
** these are non-KERI CESR Proof Signatures because it’s a guest data object.

This way KERI becomes versatile and extensible by anchoring more types of signed content. All signed SADs, KERI events and non-KERI events, become uniform — and more easily maintainable with the aid of the `cesr-proof` extension, without having to define a unique signature scheme for each protocol.

KERI experts see CESR Proof Signatures as a *necessity* to make the custom-made representation for KERI meet other features and constraints in the Virtual Credentials domain, such as complex signatures.
> # Is some other magic happening under the hood of Self-Addressing Data?

One thing is for sure: we need non-KERI self-addressing data to be (multi) signed and those signatures need to be streamed together with the rest of the data and Key Event Log and Transaction Event Log data.

![Creative Commons license — Scattered pieces](https://cdn-images-1.medium.com/max/3200/1*NUBJ72h8yrcb0FZhd2peag.png)*Creative Commons license — Scattered pieces*

**Why are we scattering encrypted pieces of data** and signatures all over the cyber universe?

Because that’s how the internet works. Data gets lost, needs to be composable between binary format and text format (readable for humans), needs to be hidden, needs to be put back as a whole, etc. And encrypted data is a special — more complex case because you can’t judge integrity and completeness at face value.

Private keys and related derivations from them (e.g. signatures) are an even higher order of ‘special case’ for security reasons, because they might control real value. If proof of control gets lost in the streaming, we might lose control over valuable assets.

Another consideration is that KERI events are meant to be exchanged over TCP or UDP and as such, the data getting “lost” and / or “fragmented” is the nature of UDP.

That is why the ‘CESR Proof Signatures’ extension is not a bolt-on :

1. it can’t be done with the smaller CESR set and mechanism

1. it offers versatility: non-KERI data can be streamed too

1. it makes Virtual Credential transaction events in KERI more efficient, because…

the extension is a necessary addition that has a language to address, or point to signatures that can be attached to different nested envelopes of data. If it’s not the raw multi-signature data that is provided in JSON or CBOR, then a pointer will point to where the raw data will be. 
The “address” is built up and parsed with the SAD Path Language and points to the place where the signatures will be provided once all pieces received are put back together. It is a transposable and composable mechanism:

1. you can put the sigs of the SADs wherever you want and relocate them to their origin or a new place (transposability)

2. you can go back and forth from binary to text and vice versa (composability)

Sam Smith, in a personal communication, shines a light on the design choices for CESR :

“Anything that must be signed must be serialized and that serialization must be reproducible. This means the field ordering must be fixed. So it’s not a unique limitation for CESR Proof Signatures. Given that we have fixed field ordering we can simplify pathing so it’s a win.” 
Other readily available and maybe more extensive alternatives have been studied. Smith: “JSONPth and JsonPtr were intended for non-cryptographic applications where field ordering is not required to be fixed.” 
Therefore CESR Proof Signatures is a ‘just-fine’ solution for new functionality that further opens doors for efficiency improvements… but that’s another article.

Now that we’ve made the decision for you that CESR Proof Signature is a great extension to CESR, and hopefully you’re still with us, sit back for a moment, put some galactic music on and try to image CESR streams floating around cyber space. Chopped into pieces, either binary or text, pointers to sigs all over the place, and real sigs in a few places attached to self-addressing data (SADs).

If you are still going strong through this article, remember the only thing I’d like to achieve is to give you the indelible image of **scattered pieces of digital signatures confidently floating around in cyberspace. **And, that these

![Creative Commons license — Confidently floating in space](https://cdn-images-1.medium.com/max/2136/1*veNmjAfwWLz1kYoANA9Wtw.jpeg)*Creative Commons license — Confidently floating in space*

particles, once received and put back together as a whole, haven’t lost a bit of their integrity, their security or their effectiveness.
> Always on the look out for striking analogies, the best I can come up with is that CESR Proof Signatures for KERI resembles what Segwit does for Bitcoin.

CESR Proof Signatures offer Nested Partial Signatures: the entire group of signatures can be transposed across envelope boundaries by changing only the root path of the group attachment code. This happens to the signatures in segregated witnesses for bitcoin too. The reason in bitcoin for designing Segwit was twofold: security and data efficiency. In CESR the reason for pointing to sigs in an *attachment* adds to security and efficiency:

1. **ability** **to stream** the serialization once the payload is signed off

1. **universality** of signature schemes (across issuance and proving of VCs)

1. **bandwidth** optimisation by limiting SAD Path Language scope

No other event streaming standard protocol has these features yet. So CESR Proof Signatures is new and unique, and joyfully so. For the first time in history we’re able to stream transposable proofs and signature data that answers both ‘who said what?’ and ‘is it true?’ questions securely for authentication problems on the web in combination with signed credentials. This is unsurpassed, as far as I know.

Let’s wrap up in style; with creator Phil Feairheller’s words:
> “A primary goal of CESR Proof Signatures is to allow any signed self-addressing data (SAD) to be streamed inline with any other CESR content.”
> “Protocols for verifiable credential issuance and proof presentation can be defined using this capability to embed the same verifiable credential SAD at and location in an enveloping exn message as appropriate for the protocol without having to define a unique signature scheme for each protocol.”
> “The [SAD Path] language accomplishes the goal of uniquely locating any path in a SAD using minimally sufficient means in a manner that allows it to be embedded in a CESR attachment as Base64. Alternative syntaxes would need to be Base64 encoded to be used in a CESR attachment in the text domain thus incurring the additional bandwidth cost of such an encoding.”
> Source: [GitHub](https://github.com/WebOfTrust/ietf-cesr-proof/blob/main/draft-pfeairheller-cesr-proof.md#transposable-signature-attachments) IETF CESR Proof
> # Oh, and one last thing for you: tune in again to [galactic music](https://www.soundsnap.com/spacesparks_cut) to perpetuate the image of CESR Proof Sigs confidently floating around in cyberspace.

**Acknowledgements**

Picture less burden more joy - Rhonda Reah -[WWW.THEWRiTECONVERSATiON.COM](http://WWW.THEWRiTECONVERSATiON.COM)

Picture [Down the Rabbit Hole — Write Right — writerightwords.com](https://www.writerightwords.com/down-the-rabbit-hole/)

[Back tot the light](https://pxhere.com/en/photo/427068), crop from Creator: Photographer:Sean D Brown, 117 Productions 2013

Picture The big Why — Styles Research: A Big List of Questions — [tinybeeman.com](http://tinybeeman.com)

Picture — Floating in space - [How Will Humans Colonize Space in the Years Ahead singularityhub.com](https://singularityhub.com/2017/11/27/how-will-humans-colonize-space-in-the-years-ahead/)

Picture Scattered pieces — [2017 | Malaysia Students malaysia-students.com](http://www.malaysia-students.com/2017/)
