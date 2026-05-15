---
layout: single
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---
{% include base_path %}

Download my CV as a PDF — or view it below.

<div style="text-align: center; margin: 0 -1.5em;">
  <iframe
    id="pdf-viewer"
    src="/assets/public_cv_hosted.pdf"
    width="100%"
    style="border: none; min-height: 700px; height: 85vh; display: block;"
    onload="resizeIframe(this)">
    <p>Your browser does not support inline PDFs. <a href="/assets/public_cv_hosted.pdf">Download CV (PDF)</a></p>
  </iframe>
</div>

<script>
  function resizeIframe(iframe) {
    try {
      var h = iframe.contentWindow.document.documentElement.scrollHeight;
      if (h > 400) iframe.style.height = h + 'px';
    } catch(e) {}
  }
</script>