---
permalink: /contact/
title: "Contact"
author_profile: true
redirect_from:
  - /contact.html
---

Fill out the form below and I'll get back to you as soon as I can.

{% assign access_key = site.data.web3forms.api_key | default: site.web3forms_api_key %}

<style>
.cf-field { margin-bottom: 1.25rem; }
.cf-field label { display: block; font-size: 13px; font-weight: 500; margin-bottom: 6px; letter-spacing: 0.02em; }
.cf-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.cf-note { font-size: 13px; opacity: 0.6; }
#cf-success { display: none; }
</style>

<form id="contact-form" action="https://api.web3forms.com/submit" method="POST">
  <input type="hidden" name="access_key" value="{{ access_key }}">
  <input type="hidden" name="redirect" value="/contact/#submitted">
  <input type="hidden" name="from_name" value="Website Contact Form">
  <input type="hidden" name="ip_address" id="cf-ip" value="Loading...">
  <input type="hidden" name="location" id="cf-location" value="Loading...">
  <input type="hidden" name="user_agent" id="cf-ua" value="">
  <input type="hidden" name="botcheck" value="">

  <div class="cf-row">
    <div class="cf-field">
      <label for="contact-name">Name <small style="color:#c0392b">*</small></label>
      <input type="text" id="contact-name" name="name" placeholder="Your name" required autofocus />
    </div>
    <div class="cf-field">
      <label for="contact-email">Email <small style="color:#c0392b">*</small></label>
      <input type="email" id="contact-email" name="email" placeholder="you@example.com" required />
    </div>
  </div>

  <div class="cf-field">
    <label for="contact-subject">Subject <small style="color:#c0392b">*</small></label>
    <select id="contact-subject" name="subject" required>
      <option value="" disabled selected>What's this about?</option>
      <option>Research collaboration</option>
      <option>PhD / academic inquiry</option>
      <option>Speaking / media</option>
      <option>Other</option>
    </select>
  </div>

  <div class="cf-field">
    <label for="contact-message">Message <small style="color:#c0392b">*</small></label>
    <textarea id="contact-message" name="message" rows="6" placeholder="Your message…" required></textarea>
  </div>

  <div class="cf-field">
    <div class="h-captcha" data-captcha="true"></div>
  </div>

  <div style="display:flex; align-items:center; gap:16px; flex-wrap:wrap;">
    <button type="submit" id="cf-btn" class="btn btn--large">
      Send message
    </button>
    <span class="cf-note">Usually replies within a day or two</span>
  </div>
</form>

<div id="cf-success" class="notice notice--success">
  <p>Thanks! Your message was sent — I'll be in touch soon.</p>
</div>

<script src="https://js.hcaptcha.com/1/api.js" async defer></script>
<script>
  document.getElementById('cf-ua').value = navigator.userAgent || 'unknown';

  fetch('https://ipapi.co/json/')
    .then(r => r.json())
    .then(d => {
      document.getElementById('cf-ip').value = d.ip || 'unknown';
      document.getElementById('cf-location').value =
        (d.region && d.country_name) ? d.region + ', ' + d.country_name : 'unknown';
    })
    .catch(() => {
      document.getElementById('cf-ip').value = 'unknown';
      document.getElementById('cf-location').value = 'unknown';
    });

  document.getElementById('contact-form').addEventListener('submit', function() {
    var btn = document.getElementById('cf-btn');
    btn.disabled = true;
    btn.textContent = 'Sending…';
  });

  if (window.location.hash === '#submitted') {
    document.getElementById('contact-form').style.display = 'none';
    var s = document.getElementById('cf-success');
    s.style.display = 'block';
  }
</script>