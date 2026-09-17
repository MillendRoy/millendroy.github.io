---
layout: about
title: about
permalink: /
subtitle: <a href='https://ieor.columbia.edu/content/millend-roy'>Ph.D. Student in Operations Research</a>, Columbia University

profile:
  align: right
  image: Millend_Profile.png
  image_circular: false # crops the image to make it circular
  # more_info: >
  #   <p>Operations Research</p>
  #   <p>Columbia University, New York, NY</p>

selected_papers: true # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page

announcements:
  enabled: false

latest_posts:
  enabled: false
---

<div markdown="1" style="text-align: justify;">

Hello! At Columbia, I am advised by the amazing [Prof. Agostino Capponi](https://www.columbia.edu/~ac3827/). My research spans statistics, machine learning, and algorithm design, with a focus on **efficient computation** and **decision-making under uncertainty**. I develop mathematical models and scalable algorithms for problems in machine learning and energy systems, and study the physical and economic factors that shape electricity markets.

Previously, I was a SCAI (Societal impact through Cloud and Artificial Intelligence) Research Fellow at Microsoft Research India, where I worked on [Project Vasudha](https://www.microsoft.com/en-us/research/project/vasudha/). I am fortunate to have been advised by [Dr. Akshay Nambi](https://www.microsoft.com/en-us/research/people/akshayn/), [Tanuja Ganu](https://www.microsoft.com/en-us/research/people/taganu/), and [Dr. Shivkumar Kalyanaraman](https://www.shivkumar.org/). I applied reinforcement learning and metaheuristic optimization to distributed energy management, worked on EV range anxiety, and helped turn research prototypes into early-stage solutions for Microsoft partners.

I received my Bachelor’s degree in Electrical Engineering from the Indian Institute of Technology (ISM), Dhanbad, where I developed my foundation in power systems. I am especially grateful to [Dr. Soham Dutta](https://scholar.google.com/citations?user=rgdHa8EAAAAJ&hl=en) and [Dr. Bhukya Krishna Naik](https://www.linkedin.com/in/bhukya-krishna-naick-7971331a4/), with whom I worked on my early research projects and whose guidance motivated me to pursue graduate studies.

Outside research, I enjoy playing cricket 🏏, table tennis 🏓, and pool 🎱. I also love sketching ✏️ - you can find some of my work in the [gallery](/gallery/). I have formal training in harmonium 🎶 and am now trying to learn the keyboard, with a little more practice this time! :)

</div>

<div class="org-logos">
  {% for org in site.data.organizations %}
    <a href="{{ org.url }}" target="_blank" rel="external nofollow noopener" title="{{ org.name }}">
      <img src="{{ org.logo | relative_url }}" alt="{{ org.name }}">
    </a>
  {% endfor %}
</div>

<style>
.org-logos {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 2rem;
  margin-top: 2rem;
  padding-top: 1.5rem;
  border-top: 1px solid rgba(128,128,128,0.2);
}
.org-logos {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 2.5rem;
  margin: 2.5rem 0 3rem;
  padding-top: 2rem;
  border-top: 1px solid rgba(128,128,128,0.2);
}
.org-logos img {
  height: 40px;
  width: auto;
  object-fit: contain;
}
.org-logos img:hover {
  filter: grayscale(0%);
  opacity: 1;
}
</style>