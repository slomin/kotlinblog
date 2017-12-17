---
layout: post
title: Speculative Attack on Blockchain Based Cryptocurrency
comments: true
---
Since the recent Bitcoin hype, I've been thinking about different types of cryptocurrencies, their design, usage etc. I came up with an idea how to severely impact some blockchain based cryptocurrency's public perception, and in the result, it's trading price. Let me just disclose that this is just speculation on my part, I don't have a will nor means to do this, and I'm definitively **not** the first person who figured this out, so this might be a kind of "warning" when you see something like this happening.

But first, let's focus how typical blockchain cryptocurrency (Bitcoin included) works. I'm not going to go into details here if you want to see a great technical explanation check out this great presentation:

<iframe width="560" height="315" src="https://www.youtube.com/embed/_160oMzblY8" frameborder="0" allowfullscreen></iframe>

You can also check [this great live demo](https://anders.com/blockchain/hash.html)

I'll focus on important features that allow this kind of "attack" and I will explain this using Bitcoin as an example. Basically, blockchain is a publicly available [ledger](https://en.wikipedia.org/wiki/Ledger) which contains all the Bitcoins ever created and all the transaction records. As I'm writing this it amassed to roughly 150 gigabytes of data. All the Bitcoins are assigned to "wallets", which are pairs of public and private cryptographic keys. The public key is stored in the ledger (when the first token transfer to this wallet happens), while the private key is stored by the owner in a secure manner. The private key allows transferring Bitcoins to another wallet.

This is really that simple. There is no overseer, all the system "cares" is that the owner has a private key to the wallet. This has several implications:

- The system relies 100% on secure cryptography.
- If the owner somehow loses the private key (it is destroyed, lost, forgotten etc) the Bitcoins are lost, forever. There is **no** way to get those bitcoins back.
- If someone else gets access to the owner's private key, this person can transfer Bitcoins within a matter of minutes. The **only** way to protect the Bitcoins when the key was compromised is to transfer them faster than the thief to another, non-compromised wallet. After stealing the money there is **no** way to get them back (there is no regulatory body, no customer support to call).
- If the owner sends money by accident/to a wrong recipient, there is no way to reverse that transaction.
- **All** the wallets with money on them are available to view for anyone on the Internet because the ledger is public. You can see all the Bitcoin transactions on a particular wallet.

The first implication is crucial. The only reason cryptocurrencies hold value is the fact they're are secure. If you undermine this perception, the value will go down.

Now let's think how secure they are? The correct answer is - we don't know for sure. Let's look at Bitcoin's protocol: it is based on [SHA-256](https://en.wikipedia.org/wiki/SHA-2) hash function, which, ironically, was introduced by the [NSA](https://en.wikipedia.org/wiki/National_Security_Agency). There is **no** mathematical proof this algorithm is secure. We only know that no one (at least in the open) was able to crack it in a practical manner. Both [SHA-1](https://en.wikipedia.org/wiki/SHA-1) and [MD5](https://en.wikipedia.org/wiki/MD5) has been broken roughly ~15 years after being introduced. The crypto behind ZCash, [zn-SNARKs](https://dl.acm.org/citation.cfm?id=2090263) was introduced in 2012 so it is **really** new. You can say the same about CryptoNote used in Bytecoin and Monero. I also encourage you to read [this article about IOTA](https://medium.com/@neha/cryptographic-vulnerabilities-in-iota-9a6a9ddc4367). Keep also in mind the rapid development of quantum computing in the recent years. If someone will tell you those cryptocurrencies are 100% hack-proof, they are lying. Maybe they are but we just don't know that right now. Also, Bitcoin protocol has been hacked before. The [CVE-2010-5139 vulnerability](https://en.bitcoin.it/wiki/Value_overflow_incident) in 2010 allowed the creation of over **184 billion bitcoins**. The blockchain had to be forked to fix that screwup. So there are precedences.

There are also now **HUGE** incentives to find vulnerabilities, as David Schwartz (Chief Cryptographer ad Ripple) said: "What we have now is a multi-billion dollar bug bounty program".

**The FUD attack**

Let's talk about the theoretical "attack". To pull this off the attackers would need some hefty amount of money "parked" in targeted cryptocurrency, IMO at least 1M$. The particular crypto price doesn't matter. All that matters is the "real" money involved (USD, EUR, GBP, RMB etc) to scare other current and potential investors. Keep in mind this money doesn't have to be wasted and can be recovered after the stunt. In an ideal case, this would be some "old money", i.e. money lying on particular wallets for a while (not transferred there just before the stunt). The attackers would then "fake" their tokens were stolen. It could be accomplished by just transferring the money to some fresh wallets. Those wallets would, of course, belong to attackers, but there is **no** way to check and prove that.

After transferring the tokens, the "attackers" would go public with this fake information in a coordinated manner. Preferably to different language speaking communities. One person would talk about it on some English speaking crypto forum. The other would go to Russian one, another would post on Chinese social media etc. This is a classic [FUD](https://en.wikipedia.org/wiki/Fear,_uncertainty_and_doubt) campaign. Those people can show their account being wiped as a proof, since as I mentioned, all the transactions are publicly available. If I were the "attacker" I would do some wallet-juggling, in the end transfer the money to couple of particular wallets and then to some more private cryptocurrency (like ZCash) so it could never be traced.

This would probably get some media attention, since it has a big "click-generating" potential: cryptocurrencies and people loosing their live savings due to some mysterious hacker. The problem is, due to most of the cryptocurrencies nature, there is **no** credible way to disprove this as a hoax. The particular cryptocurrency community/maintainers couldn't do much. They can't tell if the protocol is being compromised, they could just assure that nothing suspicious was found. To be honest after seeing this kind of news, as a holder of particular cryptocurrency I would be at least little afraid of loosing all my money.
