---
layout: post
title: Making Classical (Threshold) Signatures Post-Quantum for Single Use on a Public Ledger
description: Semester Project Fall 2021
---

Context
============

As a requirement for my 1st year in the EPFL IC doctoral school, I had to work on a research project for the duration of a semester. 
Under the supervision of Pr. Serge Vaudenay, and together with my colleague [Abdullah Talayhan](https://www.abdullahtalayhan.com) , we started this project with the idea to extend the Bitcoin P2PKH (Pay to Public Key Hash) transactions to the threshold setting. The advantage of P2PKH transactions is that it provides some sort of protection against quantum adversaries if the public-private key pair is never re-used after a transaction has been made from it, since the public key isn't published directly, but rather hidden behind a hash. Using this idea, we wanted to extend it to the threshold setting as well, while preserving both classical security and this one-time use post-quantum security. We wanted to focus on a practical and efficient approach, and therefore didn't consider post-quantum signature schemes. 

We had several goals : 
* Formalizing the security of a transform that hides the public key in a classical and quantum setting.
* Proving the security of the P2PKH transform using these security notions.
* Giving a similar transform that hides the public key for the threshold setting. 

We achieved the first goal. The classical security is captured by the well-known notion of *existential unforgeability under chosen-message attack* (EUF-CMA). The quantum security is captured by the notion of *existential forgery under key-only attack* by considering a quantum adevrsary for both the one-signer and threshold setting. This notion of security is enough in the setting where key-pairs are used only once. 

We checked the 2nd box, with a catch: P2PKH EUF-CMA security can't be proven under 2nd pre-image resistance of the hash function, but requires the stronger notion of *collision resistance*... 

This leds us to the 3rd point. Instead of extending the P2PKH transform to a threshold setting, we provide a new transform, based on uniform random masking, whose security only requires 2nd pre-image resistance for the hash function used. We also give an extension this transform to the threshold setting in two possible ways. The 1st one requires only a standard multi-party computation protocol for key generation without any multi-party hash function evaluation (which is usually a huge performance bottleneck), at the cost of an increase in public-key and signature size that is linear in the number of participants. The 2nd one provides a transform with constant public-key and signature size, but does require one multi-party hash function evaluation. 

Additionally we constructed and proved the security of a delayed signature scheme that enables practical usage of our signature primitives in a distributed ledger environment.

This project gave rise to an (eprint)[https://eprint.iacr.org/2023/420]

## Abstract 
The Bitcoin architecture heavily relies on the ECDSA signature scheme which is broken by quantum adversaries as the secret key can be computed from the public key in quantum polynomial time. To mitigate this attack, bitcoins can be paid to the hash of a public key (P2PKH). However, the first payment reveals the public key so all bitcoins attached to it must be spent at the same time (i.e. the remaining amount must be transferred to a new wallet). Some problems remain with this approach: the owners are vulnerable against rushing adversaries between the time the signature is made public and the time it is committed to the blockchain. Additionally, there is no equivalent mechanism for threshold signatures. Finally, no formal analysis of P2PKH has been done.
In this paper, we formalize the security notion of a digital signature with a hidden public key and we propose and prove the security of a generic transformation that converts a classical signature to a post-quantum one that can be used only once. We compare it with P2PKH. Namely, our proposal relies on pre-image resistance instead of collision resistance as for P2PKH, so allows for shorter hashes. Additionally, we propose the notion of a delay signature to address the problem of the rushing adversary when used with a public ledger and discuss the advantages and disadvantages of our approach. We further extend our results to threshold signatures.
