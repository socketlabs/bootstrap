---
layout: docs
title: Validation
description: Provide valuable, actionable feedback to your users with HTML5 form validation, via browser default behaviors or custom styles and JavaScript.
group: forms
toc: true
---

{{< callout warning >}}
We are aware that currently the client-side custom validation styles and tooltips are not accessible, since they are not exposed to assistive technologies. While we work on a solution, we'd recommend either using the server-side option or the default browser validation method.
{{< /callout >}}

## How it works

Here's how form validation works with Bootstrap:

- HTML form validation is applied via CSS's two pseudo-classes, `:invalid` and `:valid`. It applies to `<input>`, `<select>`, and `<textarea>` elements.
- Bootstrap scopes the `:invalid` and `:valid` styles to parent `.was-validated` class, usually applied to the `<form>`. Otherwise, any required field without a value shows up as invalid on page load. This way, you may choose when to activate them (typically after form submission is attempted).
- To reset the appearance of the form (for instance, in the case of dynamic form submissions using AJAX), remove the `.was-validated` class from the `<form>` again after submission.
- As a fallback, `.is-invalid` and `.is-valid` classes may be used instead of the pseudo-classes for [server-side validation](#server-side). They do not require a `.was-validated` parent class.
- Due to constraints in how CSS works, we cannot (at present) apply styles to a `<label>` that comes before a form control in the DOM without the help of custom JavaScript.
- All modern browsers support the [constraint validation API](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#the-constraint-validation-api), a series of JavaScript methods for validating form controls.
- Feedback messages may utilize the [browser defaults](#browser-defaults) (different for each browser, and unstylable via CSS) or our custom feedback styles with additional HTML and CSS.
- You may provide custom validity messages with `setCustomValidity` in JavaScript.

With that in mind, consider the following demos for our custom form validation styles, optional server-side classes, and browser defaults.

## Custom styles

For custom Bootstrap form validation messages, you'll need to add the data-bs-toggle="form-validation" `<form>`. This disables the browser default feedback tooltips, but still provides access to the form validation APIs in JavaScript. Try to submit the form below; our JavaScript will intercept the submit button and relay feedback to you. When attempting to submit, you'll see the `:invalid` and `:valid` styles applied to your form controls.

Custom feedback styles apply custom colors, borders, focus styles, and background icons to better communicate feedback. Background icons for `<select>`s are only available with `.form-select`, and not `.form-control`.

{{< example >}}
<form class="row g-3" data-bs-toggle="form-validation">
  <div class="col-md-4">
    <label for="validationCustom1" class="form-label">First name</label>
    <input type="text" class="form-control" id="validationCustom1" value="Mark" required data-bs-valid="Looks good!" data-bs-invalid="Please, provide a valid Name!">
  </div>
  <div class="col-md-4">
    <label for="validationCustom2" class="form-label">Last name</label>
    <input type="text" class="form-control" id="validationCustom2" value="Otto" required data-bs-valid="Looks good!">
  </div>
  <div class="col-md-4">
    <label for="validationCustom3" class="form-label">Username</label>
    <div class="input-group has-validation">
      <span class="input-group-text" id="validationCustom3-prepend">@</span>
      <input type="text" class="form-control" id="validationCustom3" aria-describedby="validationCustom3-prepend" required data-bs-invalid="Please choose a username.">
    </div>
  </div>
  <div class="col-md-6">
    <label for="validationCustom4" class="form-label">City</label>
    <input type="text" class="form-control" id="validationCustom4" required data-bs-invalid="Please provide a valid city.">
  </div>
  <div class="col-md-3">
    <label for="validationCustom5" class="form-label">State</label>
    <select class="form-select" id="validationCustom5" required data-bs-invalid="Please select a valid state.">
      <option selected disabled value="">Choose...</option>
      <option>...</option>
    </select>
  </div>
  <div class="col-md-3">
    <label for="validationCustom6" class="form-label">Zip</label>
    <input type="text" class="form-control" id="validationCustom6" required data-bs-invalid="Please provide a valid zip.">
  </div>
  <div class="col-12">
    <div class="form-check">
      <input class="form-check-input" type="checkbox" value="" id="validationCustom7" required data-bs-invalid="You must agree before submitting.">
      <label class="form-check-label" for="validationCustom7">
        Agree to terms and conditions
      </label>
    </div>
  </div>
  <div class="col-12">
    <button class="btn btn-primary" type="submit">Submit form</button>
    <button class="btn btn-danger" type="reset">Reset form</button>
  </div>
</form>
{{< /example >}}

{{< example lang="js" show_preview="false" >}}
{{< js.inline >}}
{{< /js.inline >}}
{{< /example >}}

## Browser defaults

Not interested in custom validation feedback messages or writing JavaScript to change form behaviors? All good, you can use the browser defaults. Try submitting the form below. Depending on your browser and OS, you'll see a slightly different style of feedback.

While these feedback styles cannot be styled with CSS, you can still customize the feedback text through JavaScript.

{{< example >}}
<form class="row g-3">
  <div class="col-md-4">
    <label for="validationDefault1" class="form-label">First name</label>
    <input type="text" class="form-control" id="validationDefault1" value="Mark" required>
  </div>
  <div class="col-md-4">
    <label for="validationDefault2" class="form-label">Last name</label>
    <input type="text" class="form-control" id="validationDefault2" value="Otto" required>
  </div>
  <div class="col-md-4">
    <label for="validationDefault3" class="form-label">Username</label>
    <div class="input-group">
      <span class="input-group-text" id="validationDefault3-prepend">@</span>
      <input type="text" class="form-control" id="validationDefault3"  aria-describedby="validationDefault3-prepend" required>
    </div>
  </div>
  <div class="col-md-6">
    <label for="validationDefault4" class="form-label">City</label>
    <input type="text" class="form-control" id="validationDefault4" required>
  </div>
  <div class="col-md-3">
    <label for="validationDefault5" class="form-label">State</label>
    <select class="form-select" id="validationDefault5" required>
      <option selected disabled value="">Choose...</option>
      <option>...</option>
    </select>
  </div>
  <div class="col-md-3">
    <label for="validationDefault6" class="form-label">Zip</label>
    <input type="text" class="form-control" id="validationDefault6" required>
  </div>
  <div class="col-12">
    <div class="form-check">
      <input class="form-check-input" type="checkbox" value="" id="validationDefault7" required>
      <label class="form-check-label" for="validationDefault7">
        Agree to terms and conditions
      </label>
    </div>
  </div>
  <div class="col-12">
    <button class="btn btn-primary" type="submit">Submit form</button>
  </div>
</form>
{{< /example >}}

## Server side

We recommend using client-side validation, but in case you require server-side validation, you can indicate invalid and valid form fields with `.is-invalid` and `.is-valid`. Note that `.invalid-feedback` is also supported with these classes.

For invalid fields, ensure that the invalid feedback/error message is associated with the relevant form field using `aria-describedby` (noting that this attribute allows more than one `id` to be referenced, in case the field already points to additional form text).

To fix [issues with border radii](https://github.com/twbs/bootstrap/issues/25110), input groups require an additional `.has-validation` class.

{{< example >}}
<form class="row g-3">
  <div class="col-md-4">
    <label for="validationServer1" class="form-label">First name</label>
    <input type="text" class="form-control is-valid" id="validationServer1" value="Mark" aria-describedby="validationServer1-formTip" required>
    <div id="validationServer1-formTip" class="valid-feedback">
      Looks good!
    </div>
  </div>
  <div class="col-md-4">
    <label for="validationServer2" class="form-label">Last name</label>
    <input type="text" class="form-control is-valid" id="validationServer2" value="Otto" aria-describedby="validationServer2-formTip" required>
    <div id="validationServer2-formTip" class="valid-feedback">
      Looks good!
    </div>
  </div>
  <div class="col-md-4">
    <label for="validationServer3" class="form-label">Username</label>
    <div class="input-group has-validation">
      <span class="input-group-text" id="validationServer3-prepend">@</span>
      <input type="text" class="form-control is-invalid" id="validationServer3" aria-describedby="validationServer3-prepend validationServer3-formTip" required>
      <div id="validationServer3-formTip" class="invalid-feedback">
        Please choose a username.
      </div>
    </div>
  </div>
  <div class="col-md-6">
    <label for="validationServer4" class="form-label">City</label>
    <input type="text" class="form-control is-invalid" id="validationServer4" aria-describedby="validationServer4-formTip" required>
    <div id="validationServer4-formTip" class="invalid-feedback">
      Please provide a valid city.
    </div>
  </div>
  <div class="col-md-3">
    <label for="validationServer5" class="form-label">State</label>
    <select class="form-select is-invalid" id="validationServer5" aria-describedby="validationServer5-formTip" required>
      <option selected disabled value="">Choose...</option>
      <option>...</option>
    </select>
    <div id="validationServer5-formTip" class="invalid-feedback">
      Please select a valid state.
    </div>
  </div>
  <div class="col-md-3">
    <label for="validationServer6" class="form-label">Zip</label>
    <input type="text" class="form-control is-invalid" id="validationServer6" aria-describedby="validationServer6-formTip" required>
    <div id="validationServer6-formTip" class="invalid-feedback">
      Please provide a valid zip.
    </div>
  </div>
  <div class="col-12">
    <div class="form-check">
      <input class="form-check-input is-invalid" type="checkbox" value="" id="validationServer7" aria-describedby="validationServer7-formTip" required>
      <label class="form-check-label" for="validationServer7">
        Agree to terms and conditions
      </label>
      <div id="validationServer7-formTip" class="invalid-feedback">
        You must agree before submitting.
      </div>
    </div>
  </div>
  <div class="col-12">
    <button class="btn btn-primary" type="submit">Submit form</button>
  </div>
</form>
{{< /example >}}

## Supported elements

Validation styles are available for the following form controls and components:

- `<input>`s and `<textarea>`s with `.form-control` (including up to one `.form-control` in input groups)
- `<select>`s with `.form-select`
- `.form-check`s

{{< example >}}
<form class="was-validated">
  <div class="mb-3">
    <label for="validationSupported1" class="form-label">Textarea</label>
    <textarea class="form-control is-invalid" id="validationSupported1" placeholder="Required example textarea" aria-describedby="validationSupported1-formTip" required></textarea>
    <div id="validationSupported1-formTip" class="invalid-feedback">
      Please enter a message in the textarea.
    </div>
  </div>

  <div class="form-check mb-3">
    <input type="checkbox" class="form-check-input" id="validationSupported2" aria-describedby="validationSupported2-formTip" required>
    <label class="form-check-label" for="validationSupported2">Check this checkbox</label>
    <div id="validationSupported2-formTip" class="invalid-feedback">Example invalid feedback text</div>
  </div>

  <div class="form-check">
    <input type="radio" class="form-check-input" id="validationSupported3" name="radio-stacked" required>
    <label class="form-check-label" for="validationSupported3">Toggle this radio</label>
  </div>
  <div class="form-check mb-3">
    <input type="radio" class="form-check-input" id="validationSupported4" name="radio-stacked" aria-describedby="validationSupported4-formTip" required>
    <label class="form-check-label" for="validationSupported4">Or toggle this other radio</label>
    <div id="validationSupported4-formTip" class="invalid-feedback">More example invalid feedback text</div>
  </div>

  <div class="mb-3">
    <select id="validationSupported5" class="form-select" required aria-label="select example" aria-describedby="validationSupported5-formTip">
      <option value="">Open this select menu</option>
      <option value="1">One</option>
      <option value="2">Two</option>
      <option value="3">Three</option>
    </select>
    <div id="validationSupported5-formTip" class="invalid-feedback">Example invalid select feedback</div>
  </div>

  <div class="mb-3">
    <input id="validationSupported6" type="file" class="form-control" aria-label="file example" aria-describedby="validationSupported6-formTip" required>
    <div id="validationSupported6-formTip" class="invalid-feedback">Example invalid form file feedback</div>
  </div>

  <div class="mb-3">
    <button class="btn btn-primary" type="submit" disabled>Submit form</button>
  </div>
</form>
{{< /example >}}

## Tooltips

If your form layout allows it, you can swap the `.{valid|invalid}-feedback` classes for `.{valid|invalid}-tooltip` classes to display validation feedback in a styled tooltip. Be sure to have a parent with `position: relative` on it for tooltip positioning. In the example below, our column classes have this already, but your project may require an alternative setup.

{{< example >}}
<form class="row g-3" data-bs-toggle="form-validation" data-bs-type="tooltip" >
  <div class="col-md-4 position-relative">
    <label for="validationTooltip1" class="form-label">First name</label>
    <input type="text" class="form-control" id="validationTooltip1" value="Mark" required data-bs-valid="Looks good!">
  </div>
  <div class="col-md-4 position-relative">
    <label for="validationTooltip2" class="form-label">Last name</label>
    <input type="text" class="form-control" id="validationTooltip2" value="Otto" required  data-bs-valid="Looks good!">
  </div>
  <div class="col-md-4 position-relative">
    <label for="validationTooltip3" class="form-label">Username</label>
    <div class="input-group has-validation">
      <span class="input-group-text" id="validationTooltip3-prepend">@</span>
      <input type="text" class="form-control" id="validationTooltip3" aria-describedby="validationTooltip3-prepend" required data-bs-invalid="Please choose a username.">
    </div>
  </div>
  <div class="col-md-6 position-relative">
    <label for="validationTooltip4" class="form-label">City</label>
    <input type="text" class="form-control" id="validationTooltip4" required data-bs-invalid="Please provide a valid city.">
  </div>
  <div class="col-md-3 position-relative">
    <label for="validationTooltip5" class="form-label">State</label>
    <select class="form-select" id="validationTooltip5" required data-bs-invalid="Please select a valid state.">
      <option selected disabled value="">Choose...</option>
      <option>...</option>
    </select>
  </div>
  <div class="col-md-3 position-relative">
    <label for="validationTooltip6" class="form-label">Zip</label>
    <input type="text" class="form-control" id="validationTooltip6" required data-bs-invalid="Please provide a valid zip.">
  </div>
  <div class="col-12">
    <button class="btn btn-primary" type="submit">Submit form</button>
  </div>
</form>
{{< /example >}}

## Sass

### Variables

{{< scss-docs name="form-feedback-variables" file="scss/_variables.scss" >}}

### Mixins

Two mixins are combined together, through our [loop](#loop), to generate our form validation feedback styles.

{{< scss-docs name="form-validation-mixins" file="scss/mixins/_forms.scss" >}}

### Map

This is the validation Sass map from `_variables.scss`. Override or extend this to generate different or additional states.

{{< scss-docs name="form-validation-states" file="scss/_variables.scss" >}}

Maps of `$form-validation-states` can contain three optional parameters to override tooltips and focus styles.

### Loop

Used to iterate over `$form-validation-states` map values to generate our validation styles. Any modifications to the above Sass map will be reflected in your compiled CSS via this loop.

{{< scss-docs name="form-validation-states-loop" file="scss/forms/_validation.scss" >}}

### Customizing

Validation states can be customized via Sass with the `$form-validation-states` map. Located in our `_variables.scss` file, this Sass map is how we generate the default `valid`/`invalid` validation states. Included is a nested map for customizing each state's color, icon, tooltip color, and focus shadow. While no other states are supported by browsers, those using custom styles can easily add more complex form feedback.

Please note that **we do not recommend customizing `$form-validation-states` values without also modifying the `form-validation-state` mixin**.
