---
layout: post
title: A Review on Nonce-Misuse Resistant Signatures
description: Semester Project Fall 2021
---

Context
============

At the beginining of my second semester at the EPFL IC doctoral school I wrote a small review on nonce-misuse resistant signatures. 
Below is a short introduction to the problem. 

### The implications of Nonce-Misuse
In cryptography, “nonce" stands for “number only used once". It is therefore natural to wonder what happens when that one-time use property isn't respected. 
It can happen as a result of a bad implementation or a bad randomness generator, when a counter eventually repeats, as a result of random  sampling, or as a deliberate ignorance of the protocol's specification. 
We briefly describe the implications of nonce-misuse in the context of symmetric cryptography and then in that of public-key cryptography focusing on signatures. 
In symmetric cryptography, some modes of operations require an IV, and in certain cases it is crucial that it shouldn't be re-used. This is the case, for the OFB, CTR and GCM modes in particular. 
In OFB and CTR mode, reusing an IV has the same implication as reusing a key in a Vernam cipher, since their construction is similar. This means that it will leak some information about the plaintexts, and it can be especially bad if those have low entropy. However, the problem is limited to the two sent messages. 
In GCM mode, reusing a nonce directly allows for a universal forgery. Hence, it affects the entire forthcoming communication.
In the context of public key cryptography, nonces are also essential for security. 
In particular, DSA-type signatures' security, such as DSA and ECDSA signatures heavily relies on the fact that the nonce is never re-used. Indeed, using the same nonce for two signatures under the same key-pair allows a total break by recovering the secret key solving only a linear equation. This has led to several attacks in practice, e.g. on [Sony PS3] (https://www.exophase.com/20540/hackers-describe-ps3-security-as-epic-fail-gain-unrestricted-access/) or on [Bitcoin wallets for Android devices](https://bitcoin.org/en/alert/2013-08-11-android).

