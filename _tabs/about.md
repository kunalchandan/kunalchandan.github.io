---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

Hi, I'm Kunal Chandan and this is my personal website. You can check out my resume [here](https://github.com/kunalchandan/Resume-Latex/raw/master/Resume/Resume-Clean/chandan.pdf)

{% assign filenames = "https://raw.githubusercontent.com/kunalchandan/Resume-Latex/master/Resume/Resume-Clean/render-1.png,https://raw.githubusercontent.com/kunalchandan/Resume-Latex/master/Resume/Resume-Clean/render-2.png" | split: "," %}
<div class ="image-gallery">
{% for name in filenames %}
    <div class="box">
    <a href="{{ name }}">
      <img src="{{ name }} " alt="{{ name }}"  class="img-gallery" />
     </a>
    </div>
 {% endfor %}
</div>