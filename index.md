---
layout: default
---

<body>
  <div class="index-wrapper">
    <div class="aside">
      <div class="info-card">
        <h1>ljh</h1>
        <!--a href="http://weibo.com/ljh/" target="_blank"><img src="http://www.weibo.com/favicon.ico" alt="" width="25"/></a>
        <a href="http://www.douban.com/people/ljh/" target="_blank"><img src="http://www.douban.com/favicon.ico" alt="" width="22"/></a>
        <a href="http://instagram.com/ljh/" target="_blank"><img src="http://d36xtkk24g8jdx.cloudfront.net/bluebar/00c6602/images/ico/favicon.ico" alt="" width="22"/></a-->
      </div>
     
      
   </div>
    <script src="particles.js"></script> 
     <div id="particles-js"></div>
       <!-- particles.js lib (JavaScript CodePen settings): https://github.com/VincentGarreau/particles.js -->
    particlesJS.load('particles-js', 'particles.json', function() {
     console.log('callback - particles.js config loaded');
    });
    
    <div class="index-content">
      <ul class="artical-list">
        {% for post in site.categories.blog %}
        <li>
          <a href="{{ post.url }}" class="title">{{ post.title }}</a>
          <div class="title-desc">{{ post.description }}</div>
        </li>
        {% endfor %}
      </ul>
    </div>
  </div>
</body>
