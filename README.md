# Welcome to FIPS 140: the non-awesome parts


### Caveats

* These resources and opinions are wholly those of the author/contributor, and do not represent those of any other entity
* Encryption absolutely _does_ matter, but the FIPS 140-3/140-3 notion of encryption does not overlay with real-world uses of encryption and the needs of secure, scalable systems.
* FIPS 140 absolutely was awesome in 1994, but its awesomeness 30 years later is, well, debateable.
* The good people at NIST are doing the best they can with the budget and regulatory framework they have -- nothing here should cast any doubt on their dedication and professionalism.

## History

After asking on Slacks and [Fediverse](https://infosec.exchange/@pburkholder/110482715387961603) if there was a compendium of the issues with FIPS 140, and not finding any, I've started this.

## Resources

https://hackernoon.com/the-trouble-with-fips - (Still needs a full annotation)
> [T]hey had to make a version of their software that was FIPS-compliant in which they turned off everything that was novel and interesting about their product. They used shared keys or left things unencrypted to meet the standards. and it turns out you can have unencrypted data that is FIPS compliant while encrypting it runs afoul of the standard.

https://crypto.stackexchange.com/questions/96235/why-is-fips-140-2-compliance-controversial - (thread started November 2021 - lots of  references, some may be useful.)

https://blogs.oracle.com/solaris/post/is-fips-140-2-actively-harmful-to-software - 2014 blog post (referenced on FIPS 140 wikipedia page)

https://twitter.com/colmmacc/status/1505927029371199490 - Colm MacCárthaigh thread on FIPS. 


### YubiCo

https://www.yubico.com/support/issue-rating-system/security-advisories/ysa-2019-02/ - Example of FIPS-140 product having issues the mainline doesn't.

 * chalk:
yubico's fips debacle was fun. iirc, they forgot to clear out their test vectors on boot. low entropy on the first couple of signing operations. if you did things correctly (fips hardware & unplug it when not in use), you were actually worse off than otherwise.
* Alex G: I'll add that many of the underlying crypto specs aren't as good as they should be. For example, the Yubikey FIPS debacle for EC is telling. At the time (don't know if it's been fixed) the EC spec required that k be generated by a CSPRNG, and only a CSPRNG. It did not allow either deterministic k, or CSPRNG XOR deterministic, which would have significantly mitigated the issue.

## Some quotes

From ReaperHulk elsewhere..
> I've been meaning to write this for a while. A non-exhaustive list in no particular order with some ranting interspersed:
> FIPS incorporates newer algorithms very slowly. FIPS 186-5 (EdDSA) took nearly 4 years to be accepted and since its acceptance ~4-6 months ago no lab has figured out how to evaluate it, so it effectively still cannot be used
> Lab evaluations are glacial. Think months to contract, months to evaluate, and up to a year until the certificate is issued. This results in many conversations where you end up agreeing that presence on MIP (module in process) is sufficient.
> NIST will sunset things and move certificates to historical with ~1 year notice, which makes the concept of a 5 year cert kind of nonsense.
> The 140-2 to 140-3 transition involves a lot of churn around RNGs, etc that does not appear to provide much (any?) value beyond taking an immense amount of time.
> NIST thinks in terms of hardware. This results in requirements like the startup self-hashing requirement, which causes all sorts of problems for static linking (check out boringssl's delocate and https://boringssl.googlesource.com/boringssl/+/refs/heads/master/crypto/fipsmodule/FIPS.md for some background)
> The FIPS boundary is contentious. In an ideal world you'd shove your FIPS crypto into one small, immutable object, and then that never changes. This is what the US govt wishes was true. However, things are not actually built this way. For example, no one (to my knowledge) has ever managed to draw a FIPS boundary on kernel crypto that isn't just the entire damned kernel (you would think the crypto ko would work, but apparently not?)
> I'm out of time for the moment, but I can go on :slightly_smiling_face: NIST is attempting to fix some of this with increased test automation, etc but it's unclear that this is going to speed up validations. In a sane world I could get things validated so quickly that I would simply validate every small patch and everyone would be happy.
> In the world of the real, every part of the US govt ends up holding its own opinion on how strict their FIPS must be and it's up to the vendor to negotiate and determine the balance between a fully validated module and one that gets software updatesk

From Rands Leadership:

> Jen C:  Kind of sums up experience from the previous SaaS life. FIPS 140-2 was always going to be a hard no for us because we unapologetically used versions of things that once held FIPS cert but newer arguably more secure  versions hadn't been certified because the process was a P.I.T.A. and ROI didn't make a compelling case.
> jeremyc: Yeah like no Java 17+ for anything FIPS because the Bouncy Castle version that supports it isn’t FIPS certified yet. Elasticsearch 8 requires JVM 17+, and Elasticsearch 7 is EOL in August.  So…. :blob-dizzy: People who want FIPS also don’t want you to run EOL software…… (edited) 

GoLang and loss of memory safety when using OpenSSL (not sure about BoringSSL)
> Brindle: yea, so with a pure Go crypto implementation you get Go's memory safety guarantees but once you swap that out for an openssl C module the memory safety is lost while inside openssl code, and we all know how secure openssl has proven itself to be :sarcasm:

## FIPS explainers, clarifiers

https://www.safelogic.com/blog/inside-fips-inside - Walt Paley seems to have some good advice to offer.

https://boringssl.googlesource.com/boringssl/+/refs/heads/master/crypto/fipsmodule/FIPS.md - how google implements fips 140-2 in boringSSL

## Some example crypto flubs that FIPS-140 wouldn't help with

https://xkcd.com/1354/ - Heartbleed

## Tales from the trenches

