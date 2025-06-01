---
layout: page
title: XPLORER
description: a deformable aerial robot for "tactile-based exploration, mapping and navigation"
img: assets/img/xplorer.jpg
importance: 3
category: work
related_publications: true

---

XPLORER is another version of SQUEEZE. It is deformable and used to demonstrates the benefits of compliance in aerial-physical interaction tasks of mapping and navigation in unknown, cluttered environments. {% cite patnaik2023tactile %}

### 🎥 Watch XPLORER in Action

<div class="row justify-content-sm-center">
  <div class="col-sm mt-3 mt-md-0">
    <div class="embed-responsive embed-responsive-16by9">
      <iframe id="xplorer-video"
              src="https://player.vimeo.com/video/1089527111?h=7cc8083ef2"
              width="100%" height="315" frameborder="0"
              allow="autoplay; fullscreen; picture-in-picture" allowfullscreen>
      </iframe>
    </div>
    <div class="caption mt-3" style="font-size: 0.9rem;">
      <strong>🎯 Timestamped Highlights</strong><br>
      <ul style="margin-top: 0.5rem;">
        <li><a href="#" data-seek="9">Benefits of a deformable chassis (00:09–00:16)</a></li>
        <li><a href="#" data-seek="41">Interaction control yields to disturbance (00:41–00:46)</a></li>
        <li><a href="#" data-seek="62">Pushes a box without losing contact (01:02–01:10)</a></li>
        <li><a href="#" data-seek="165">Tactile exploration of a wall (02:45–03:12)</a></li>
        <li><a href="#" data-seek="205">Tactile mapping of a box (03:25–04:03)</a></li>
        <li><a href="#" data-seek="251">Tactile mapping of pipe & trash can (04:11–05:14)</a></li>
        <li><a href="#" data-seek="428">Failed attempts by rigid drone (07:08–07:27)</a></li>
        <li><a href="#" data-seek="498">New ricocheting maneuver (08:18–08:30)</a></li>
      </ul>
    </div>
  </div>
</div>

<script src="https://player.vimeo.com/api/player.js"></script>
<script>
  document.addEventListener("DOMContentLoaded", function () {
    const iframe = document.querySelector('#xplorer-video');
    const player = new Vimeo.Player(iframe);
    document.querySelectorAll('[data-seek]').forEach(link => {
      link.addEventListener('click', function (e) {
        e.preventDefault();
        const seconds = parseInt(this.getAttribute('data-seek'));
        player.setCurrentTime(seconds).then(() => {
          player.play();
        });
      });
    });
  });
</script>
