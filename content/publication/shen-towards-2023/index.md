---
title: "Towards Automated Identification of Layering Violations in Embedded Applications (WIP)"
date: 2023-06-01
publishDate: 2023-06-20T03:42:24.640114Z
authors: ["Mingjie Shen", "James C. Davis", "Aravind Machiry"]
publication_types: ["1"]
abstract: "For portability, embedded systems software follows a layered design to reduce dependence on particular hardware behavior. We consider the problem of identifying layering violations: instances where the embedded application accesses non-adjacent layers. This paper presents our preliminary work to detect a class of layering violations called Non Conventional MMIO Accesses (NCMAs). We find them by searching for direct Memory Mapped Input Output (MMIO) accesses made outside of the Hardware Abstraction Layer (HAL). For evaluation, we curated a list of 988 applications spanning 5 Real Time Operating Systems (RTOSes) – the first large dataset of compilable embedded applications. Our system identified 369 NCMAs. We reported these issues to the corresponding developers and found interesting reasons for committing layering violations. We have open-sourced our tool and the collected dataset to foster future research."
featured: false
publication: "*Proceedings of the 24th ACM SIGPLAN/SIGBED International Conference on Languages, Compilers, and Tools for Embedded Systems (LCTES)*"
tags: ["Embedded Systems", "Firmware", "Hardware Abstraction Layer", "Portability", "Static Analysis"]
doi: "10.1145/3589610.3596271"
---

