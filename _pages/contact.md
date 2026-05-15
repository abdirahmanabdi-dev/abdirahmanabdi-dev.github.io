---
permalink: /contact/
title: "Contact"
author_profile: true
redirect_from:
  - /contact.html
---

Use the form below to send me a message. The email will include your message, browser user agent, IP address, and estimated location so I can identify spam submissions.

{% assign access_key = site.data.web3forms.api_key | default: site.web3forms_api_key %}
<form id="contact-form" class="form" action="https://api.web3forms.com/submit" method="POST">
  <input type="hidden" name="access_key" value="{{ access_key }}">
  <input type="hidden" name="subject" value="New website contact message">
  <input type="hidden" name="redirect" value="/contact/#submitted">
  <input type="hidden" name="email" value="no-reply@abdirahmanabdi-dev.github.io">
  <input type="hidden" name="captcha" value="true">
  <input type="hidden" name="ip_address" id="contact-form-ip" value="Loading...">
  <input type="hidden" name="location" id="contact-form-location" value="Loading...">
  <input type="hidden" name="user_agent" id="contact-form-useragent" value="">
  <input type="hidden" name="botcheck" id="contact-form-bot-field" value="">

  <fieldset>
    <label for="contact-name">Your name <small class="required">*</small></label>
    <input type="text" id="contact-name" name="name" required autofocus />
  </fieldset>

  <fieldset>
    <label for="contact-message">Message <small class="required">*</small></label>
    <textarea id="contact-message" name="message" rows="6" required></textarea>
  </fieldset>

  <p class="small">The email will include your message plus visitor IP, estimated location, and browser user agent.</p>

  <fieldset>
    <button type="submit" class="btn btn--large">Send message</button>
  </fieldset>
</form>

<div id="contact-form-status" class="notice notice--success hidden" style="display: none;">
  <p>Thanks! Your message was submitted successfully.</p>
</div>

<script>
  var userAgentField = document.getElementById('contact-form-useragent');
  if (userAgentField) {
    userAgentField.value = navigator.userAgent || 'unknown';
  }

  function updateContactDetails(ip, region, country) {
    var ipField = document.getElementById('contact-form-ip');
    var locationField = document.getElementById('contact-form-location');
    if (ipField) ipField.value = ip || 'unknown';
    if (locationField) locationField.value = (region && country) ? region + ', ' + country : 'unknown';
  }

  fetch('https://ipapi.co/json/')
    .then(function(response) { return response.json(); })
    .then(function(data) {
      updateContactDetails(data.ip, data.region, data.country_name);
    })
    .catch(function() {
      updateContactDetails('unknown', 'unknown', 'unknown');
    });

  if (window.location.hash === '#submitted') {
    var status = document.getElementById('contact-form-status');
    if (status) {
      status.style.display = 'block';
      status.classList.remove('hidden');
    }
  }
</script>
