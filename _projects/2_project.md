---
layout: post
title: Making Classical Signatures Post-Quantum 
description: Semester Project Fall 2021
---

Context
============

As a requirement for my 1st year in the EPFL IC doctoral school, I had to work on a research project for the duration of a semester. 
Under the supervision of Pr. Serge Vaudenay, and together with my colleague Abdullah Talayhan, we started this project with the idea to extend the Bitcoin P2PKH (Pay to Public Key Hash) transactions to the threshold setting. The advantage of P2PKH transactions is that it provides some sort of protection against quantum adversaries if the public-private key pair is never re-used after a transaction has been made from it, since the public key isn't published directly, but rather hidden behind a hash. Using this idea, we wanted to extend it to the threshold setting as well, while preserving both classical security and this one-time use post-quantum security. We wanted to focus on a practical and efficient approach, and therefore didn't consider post-quantum signature schemes. 

We had several goals : 
* Formalizing the security of a transform that hides the public key in a classical and quantum setting.
* Proving the security of the P2PKH transform using these security notions.
* Give a similar transform that hides the public key for the threshold setting. 

We checked the 1st box : The classical security is captured by the well-known notion of *existential unforgeability under chosen-message attack* (EUF-CMA). We define a new notion of *zero-time quantum unforgeability* (0-QEUF) for both the one-signer and threshold setting, that captures the fact that the key-pairs are used only once. 
We checked the 2nd box, with a catch: P2PKH EUF-CMA security can't be proven under 2nd pre-image resistance of the hash function, but requires the stronger notion of *collision resistance*... 
This led us to check the 3rd box, in a slightly different way. Indeed, instead of extending the P2PKH transform to a threshold setting, we provide a new transform, based on uniform random masking, whose security only requires 2nd pre-image resistance for the hash function used. We also give an extension this transform to the threshold setting in two possible ways. The 1st one requires only a standard multi-party computation protocol for key generation without any multi-party hash function evaluation (which is usually a huge performance bottleneck), at the cost of an increase in public-key and signature size that is linear in the number of participants. The 2nd one provides a transform with constant public-key and signature size, but does require one multi-party hash function evaluation. 
Additionally we checked another box that wasn't present in the beginning by constructing and proving the security of a delayed signature scheme that enables practical usage of our signature primitives in a distributed ledger environment.

You can find below the abstract of the paper. Contact me if you would like to read the full paper.



## Abstract 
The Bitcoin architecture heavily relies on the ECDSA signature scheme which is badly broken by quantum adversaries as the secret key can be computed from the public key in quantum polynomial time. To mitigate this attack, bitcoins can be paid to the hash of a public key (P2PKH). This approach suffers from several problems: the first payment reveals the public key so all bitcoins attached to it must be spent at the same time (i.e. the remaining amount must be transferred to a new wallet), the owners remain vulnerable against rushing adversaries between the time the signature is made public and the time it is commit- ted to the blockchain, and there is no equivalent mechanism for threshold signatures. Besides, no formal analysis of P2PKH has been done. In this paper, we formalize the security notion of a *digital signature with a hidden public key*, we propose and prove the security of a generic transformation that converts a classical signature to a post-quantum one. We compare it with P2PKH and we extend it to threshold signatures. Additionally, we propose the notion of a *delay signature* to solve the problem of the rushing adversary when used with a public ledger. Our solution with a single signer relies on a secure hash function. Extension to threshold sig- natures additionally requires a secure multi-party computation protocol for the modified key generation algorithm.
