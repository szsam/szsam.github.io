---
layout: about
title: about
permalink: /
subtitle: PhD student @ <a href='https://engineering.purdue.edu/ECE'>Purdue ECE</a>

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular

selected_papers: true # includes a list of papers marked as "selected={true}"
social: false # social icons are shown in the navbar (enable_navbar_social in _config.yml)

announcements:
  enabled: true # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: false
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---

<style>
  @media (min-width: 576px) {
    .profile {
      width: 22%;
    }
  }
  .post h2 > a {
    text-transform: capitalize;
  }
</style>

I am a PhD student in the [Elmore Family School of Electrical and Computer Engineering](https://engineering.purdue.edu/ECE) at [Purdue University](https://www.purdue.edu/), advised by [Prof. Aravind Machiry](https://machiry.github.io/). Before Purdue, I received my Bachelor's degree in Computer Science and Technology from [Nanjing University](https://www.nju.edu.cn/).

My research interests span **software security**, **static program analysis**, and **AI for software engineering**, with a focus on making static analysis more effective for large, real-world software systems. I study how static analysis tools are used in practice and why they fall short on large codebases ([ISSTA 2025](https://doi.org/10.1145/3728923), [ICISS 2024](https://doi.org/10.1007/978-3-031-80020-7_13)). Motivated by these practical challenges, I explore how AI agents can improve the **precision, adaptability, and automation** of static analysis. My recent work includes using tool-augmented LLM agents to filter false positives from SAST tools ([RAID 2026]({{ '/assets/pdf/shen2026democratizing.pdf' | relative_url }})), generating repository-specific CodeQL queries for vulnerability discovery, and learning symbolic program-transformation rules to automate large-scale collateral evolution.

My research has practical impact beyond papers. Applying static analysis to over 250 open-source embedded projects uncovered more than 700 defects, over half of which were confirmed by maintainers. I submitted patches for many of them, and over 100 of those patches have been [merged upstream]({{ '/impact/' | relative_url }}) into projects including Apache NuttX, Contiki-NG, Mbed OS, RIOT, and SDL; maintainers fixed further reported bugs themselves.

I am currently looking for full-time positions in industry. If you think I would be a good fit for your team, please get in touch by email.
