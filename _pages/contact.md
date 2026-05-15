---
permalink: /contact/
title: "Contact"
author_profile: true
redirect_from:
  - /contact.html
---

{% assign web3forms = site.data.web3forms %}

<div class="page__content">

## Contact me

Use the form below to send a message. The form is submitted through Web3Forms, and the email will include the typed message plus visitor IP, estimated location, and browser user agent.

{% assign access_key = site.data.web3forms.api_key | default: site.web3forms_api_key %}
  <form id="contact-form" class="form" action="https://api.web3forms.com/submit" method="POST">
    <input type="hidden" name="access_key" value="{{ access_key }}">
    {% unless access_key %}
      <div class="alert">
        Web3Forms is not configured. Copy `_data/web3forms.example.yml` to `_data/web3forms.yml`, add your Web3Forms access key, and keep `_data/web3forms.yml` out of git. For automatic live deployment, make sure your build environment provides the secret or generates the file at build time.
      </div>
    {% endunless %}

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

    <p class="small">The email will include the message above plus the visitor IP, estimated location, and browser user agent.</p>

    <fieldset>
      <button type="submit" class="btn btn--large">Send message</button>
    </fieldset>
  </form>

  <div id="contact-form-status" class="hidden">
    <p>Thanks! Your message was submitted.</p>
  </div>

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

  var status = document.getElementById('contact-form-status');
  if (window.location.hash === '#submitted' && status) {
    status.classList.remove('hidden');
  }
</script>
