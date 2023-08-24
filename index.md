---
author_profile: false

layout: splash
permalink: /
hidden: true

excerpt:
  Ready for professional for visual technology ?!
header:
  overlay_color: "#EEEEEE"
  #overlay_filter: linear-gradient(rgba(85, 145, 197, 0.3), rgba(238, 238, 238, 0.3))
  overlay_filter: rgba(0, 0, 0, 0.3)
  overlay_image: /assets/images/wordcloud8.png
  actions:
    - label: "<i class='fas fa-thumbs-up'></i> Join us"
      url: "mailto:korfriend@gmail.com"
      
# bundle exec jekyll serve
# https://mmistakes.github.io/minimal-mistakes/about/ 
---
{% assign home = site.pages | where: 'name','home.md' %}
{{home}}

<script>

</script>