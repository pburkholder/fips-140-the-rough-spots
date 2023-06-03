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

https://www.yubico.com/support/issue-rating-system/security-advisories/ysa-2019-02/ - Example of FIPS-140 product having issues the mainline doesn't.


## FIPS explainers, clarifiers

https://www.safelogic.com/blog/inside-fips-inside - Walt Paley seems to have some good advice to offer.

## Some example crypto flubs that FIPS-140 wouldn't help with

https://xkcd.com/1354/ - Heartbleed

## Tales from the trenches

