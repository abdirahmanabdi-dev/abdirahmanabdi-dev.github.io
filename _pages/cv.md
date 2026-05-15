---
layout: single
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---
{% include base_path %}

Download my CV as a PDF:

<div style="text-align: center;">
  <iframe 
    id="pdf-viewer"
    src="/assets/public_cv_hosted.pdf"
    width="90%"
    style="border: none; min-height: 600px; display: block; margin: 0 auto;"
    onload="resizeIframe(this)">
    <p>Your browser does not support inline PDFs. <a href="/assets/public_cv_hosted.pdf">Download CV (PDF)</a></p>
  </iframe>
</div>

<script>
  function resizeIframe(iframe) {
    try {
      iframe.style.height = iframe.contentWindow.document.documentElement.scrollHeight + 'px';
    } catch(e) {
      // Cross-origin fallback — set a tall fixed height
      iframe.style.height = '1100px';
    }
  }
</script>