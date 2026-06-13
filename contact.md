---
layout: single
permalink: /contact/
classes: contact-container
---

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

<div class="container my-5">

  <!-- Step 1 -->
  <div id="step1" class="form-step">
    <h2 class="mb-3">Basic Information</h2>
    <p class="text-muted mb-4">We need a few details to begin.</p>

    <div class="mb-3">
      <label class="form-label">Work Email</label>
      <input type="email" id="email" class="form-control" required>
    </div>

    <div class="mb-3">
      <label class="form-label">Country / Region</label>
      <select id="country" class="form-select"></select>
    </div> <!-- FIXED: this closing div was missing -->

    <button class="btn btn-dark" onclick="nextStep(1)">Continue</button>
  </div>

  <!-- Step 2 -->
  <div id="step2" class="form-step d-none">
    <h2 class="mb-3">Your Details</h2>
    <p class="text-muted mb-4">Tell us more so we can understand your needs.</p>

    <div class="row">
      <div class="col-md-6 mb-3">
        <label class="form-label">First Name</label>
        <input type="text" id="fname" class="form-control" required>
      </div>

      <div class="col-md-6 mb-3">
        <label class="form-label">Last Name</label>
        <input type="text" id="lname" class="form-control" required>
      </div>
    </div>

    <div class="mb-3">
      <label class="form-label">Message</label>
      <textarea id="message" class="form-control" rows="4"></textarea>
    </div>

    <!-- NEW: Anything else? -->
    <div class="mb-3">
      <label class="form-label">Anything else? <span class="text-muted">(Optional)</span></label>
      <textarea id="extra" class="form-control" rows="4" placeholder="Tell us more about your coverage universe, AUM exposure to tech, and data consumption needs."></textarea>
    </div>

    <button class="btn btn-dark" onclick="nextStep(2)">Submit</button>
  </div>

  <!-- Step 3 -->
  <div id="step3" class="form-step d-none text-center">
    <h2 class="mb-3">Thank You</h2>
    <p class="text-muted">We’ll get back to you soon.</p>

    <!-- NEW FOOTER TEXT -->
    <p class="mt-4 text-muted small">
      Please fill out this form, and we'll reach out to you if we're able to support you.  
      If not, we'll be in touch when we're ready to open up access more broadly soon.
    </p>

    <p class="text-muted small">
      You may receive marketing communications including product updates, industry news and events.  
      You can <a href="#" class="text-decoration-underline">unsubscribe</a> at any time.
    </p>
  </div>

</div>

<script>
function nextStep(step) {
  document.getElementById("step" + step).classList.add("d-none");
  document.getElementById("step" + (step + 1)).classList.remove("d-none");
}

fetch("https://raw.githubusercontent.com/lukes/ISO-3166-Countries-with-Regional-Codes/master/all/all.json")
  .then(res => res.json())
  .then(data => {
    const select = document.getElementById("country");
    data.sort((a, b) => a.name.localeCompare(b.name));
    data.forEach(c => {
      const opt = document.createElement("option");
      opt.value = c["alpha-2"];
      opt.textContent = c.name;
      select.appendChild(opt);
    });
  });
</script>