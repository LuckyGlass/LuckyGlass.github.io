---
layout: about
title: About
permalink: /
subtitle: <a href="https://sai.pku.edu.cn/znxyenglish">School of Intelligence Science and Technology</a>. Peking University.

profile:
  align: right
  image: prof_pic.jpg
  image_circular: true # crops the image to make it circular
  more_info: >
    <p>Peking University</p>
    <p>Beijing, China</p>
    <p class="profile-social">
      <a class="ps-icon" href="mailto:ysmao_lumen@outlook.com" aria-label="Email"><i class="fa-solid fa-envelope"></i></a>
      <span class="ps-sep">|</span>
      <a href="mailto:ysmao_lumen@outlook.com">ysmao_lumen@outlook.com</a>
    </p>
    <p class="profile-social">
      <a class="ps-icon" href="https://github.com/LuckyGlass" aria-label="GitHub" target="_blank" rel="noopener noreferrer"><i class="fa-brands fa-github"></i></a>
      <span class="ps-sep">|</span>
      <a href="https://github.com/LuckyGlass" target="_blank" rel="noopener noreferrer">github.com/LuckyGlass</a>
    </p>

selected_papers: false # includes a list of papers marked as "selected={true}"
social: false # includes social icons at the bottom of the page

announcements:
  enabled: false # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: true # includes a list of blog posts
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---

Yansheng Mao is a Ph.D. student in the School of Intelligence Science and Technology at Peking University, advised by [Muhan Zhang](https://muhanzhang.github.io/) in [Μμ Lab](https://mulabpku.com/). He studies large language models, especially training infrastructure.

He received his bachelor's degree from the School of Electronics Engineering and Computer Science at Peking University in 2026, where he was a member of the Zhi Class, a special class for excellent students majoring in artificial intelligence, and was awarded the Zhi Class scholarship in 2024 and 2025.

Since its founding in 2026, he has also been a member of the founding team of Norizon (无涯智远), an early-stage AI startup in Beijing, where he is responsible for the company's training infrastructure.

## Research Interests

<div class="about-interests">
  <div class="about-interest-card">
    <h3>Training Infrastructure</h3>
    <p>
      I'm currently exploring the systems side of large model training, focusing on training frameworks such as
      Megatron-LM and the parallelism strategies (data, tensor, pipeline, and sequence parallelism) that scale
      training across large GPU clusters. As a planned next step, I aim to go a layer lower and work on
      high-performance operators and kernels.
    </p>
  </div>

  <div class="about-interest-card">
    <h3>Recursive Self-Improvement (RSI)</h3>
    <p>
      Models that keep learning after deployment, internalizing verified experience into parameters as reusable
      capabilities (in-parameter learning), with improved capability in turn accelerating further learning. I'm
      interested in making this loop near real time — e.g., hypernetworks that generate weight updates in a
      single forward pass — and in sustaining long-term growth without forgetting or interference.
    </p>
  </div>
</div>
