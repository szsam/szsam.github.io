---
title: "An Empirical Study on the Use of Static Analysis Tools in Open Source Embedded Software"
date: 2023-09-30
#publishDate: 2023-06-20T03:42:24.640114Z
authors: [admin, "Akul Pillai", "Brian A. Yuan", "James C. Davis", "Aravind Machiry"]
publication_types: ["1"]
abstract: "This paper performs the first study to understand the prevalence, challenges, and effectiveness of using Static Application Security Testing (SAST) tools on Open-Source Embedded Software (EMBOSS) repositories. We collect a corpus of 258 of the most popular EMBOSS projects, representing 13 distinct categories such as real-time operating systems, network stacks, and applications. To understand the current use of SAST tools on EMBOSS, we measured this corpus and surveyed developers. To understand the challenges and effectiveness of using SAST tools on EMBOSS projects, we applied these tools to the projects in our corpus. We report that almost none of these projects (just 3%) use SAST tools beyond those baked into the compiler, and developers give rationales such as ineffectiveness and false positives. In applying SAST tools ourselves, we show that minimal engineering effort and project expertise are needed to apply many tools to a given EMBOSS project. GitHub's CodeQL was the most effective SAST tool -- using its built-in security checks we found a total of 540 defects (with a false positive rate of 23%) across the 258 projects, with 399 (74%) likely security vulnerabilities, including in projects maintained by Microsoft, Amazon, and the Apache Foundation. EMBOSS engineers have confirmed 273 (51%) of these defects, mainly by accepting our pull requests. Two CVEs were issued. In summary, we urge EMBOSS engineers to adopt the current generation of SAST tools, which offer low false positive rates and are effective at finding security-relevant defects."
featured: true
#publication: "*Proceedings of the 24th ACM SIGPLAN/SIGBED International Conference on Languages, Compilers, and Tools for Embedded Systems (LCTES)*"
tags: ["Embedded Systems", "Empirical Software Engineering", "Static Application Security Testing (SAST)"]
doi: "10.48550/arXiv.2310.00205"
#url_slides: 'LCTES-paper9.pptx'
#url_video: 'https://www.youtube.com/watch?v=Bl0yquGFAM0&list=LL&index=4&t=3231s'
#url_code: 'https://github.com/RTOSExploration/lctes2023-artifact'
url_poster: 'sast-poster.pdf'
---

