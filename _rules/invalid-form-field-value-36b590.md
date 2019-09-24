---
id: 36b590
name: Invalid form field value
rule_type: atomic

description: |
  This rule checks that text descriptions are provided when the user completes a form field with information that is not an allowed value or using a not allowed format

accessibility_requirements: # Remove whatever is not applicable
  wcag-technique:G84: # Providing a text description when the user provides information that is not in the list of allowed values
    forConformance: false
    failed: not satisfied
    passed: satisfied
    inapplicable: further testing needed

  wcag-technique:G85: # Providing a text description when user input falls outside the required format or values
    forConformance: false
    failed: not satisfied
    passed: satisfied
    inapplicable: further testing needed

input_aspects:
  - DOM Tree
  - CSS Styling
  - Language

authors:
  - Carlos Duarte
  - João Vicente
---

## Applicability

The rule applies to each HTML or SVG element that has one of the following [semantic roles][semantic role]: `checkbox`, `combobox` (`select` elements), `listbox`, `menuitemcheckbox`, `menuitemradio`, `radio`, `searchbox`, `slider`, `spinbutton`, `switch` and `textbox`, that belongs to a [form element](https://www.w3.org/TR/html52/sec-forms.html#the-form-element).

**Note**: The list of applicable [semantic roles][semantic role] is derived by taking all the [ARIA 1.1](https://www.w3.org/TR/wai-aria-1.1/) roles that:

- inherit from the [abstract](https://www.w3.org/TR/wai-aria/#abstract_roles) `input` or `select` role, and
- do not have a [required context](https://www.w3.org/TR/wai-aria/#scope) role that itself inherits from one of those roles.

## Expectation 1

After [user completion](#completed-input-field) of the target element or triggering the submission of the form, if the target element does not meet the instructions provided for it, a message is presented to the user.

Note: Instructions for an [input element](https://www.w3.org/TR/html52/sec-forms.html#the-input-element) include information that is required by the Web page, the data format and possible values. The instructions can be presented to the user in several ways, including:

- Text content placed visually in the vicinity of the [input element](https://www.w3.org/TR/html52/sec-forms.html#the-input-element)
- The accessible description of the [input element](https://www.w3.org/TR/html52/sec-forms.html#the-input-element)
- A tooltip displayed when the [input element](https://www.w3.org/TR/html52/sec-forms.html#the-input-element) is [focused](#focusable)
- Text content accessible through an help button or similar

## Expectation 2

The content of the message is [visible](#visible) and [included in the accessibility tree](included-in-the-accessibility-tree), and identifies the [input error](https://www.w3.org/TR/WCAG21/#dfn-input-error).

## Assumptions

_There are currently no assumptions_

## Accessibility Support

_There are no major accessibility support issues known for this rule._

## Background

- [G84: Providing a text description when the user provides information that is not in the list of allowed values](https://www.w3.org/WAI/WCAG21/Techniques/general/G84)
- [G85: Providing a text description when user input falls outside the required format or values](https://www.w3.org/WAI/WCAG21/Techniques/general/G85)

## Test Cases

### Passed

#### Passed Example 1

The error message provided in the vicinity of the `input` element identifies the [input error](https://www.w3.org/TR/WCAG21/#dfn-input-error). Instructions are provided in the vicinity of the `input` element.

```html
<script>
    function processForm() {
        document.getElementById('error').innerText = "";
        var age = document.getElementById('age').value;
        console.log(isNaN(age));
        if (!age || isNaN(age)) {
            document.getElementById('error').innerText = "Age must be a number";
        } else if (age < 1) {
            document.getElementById('error').innerText = "Age must be positive";
        }
    }
</script>

<form>
    <label for="age">Age (years)</label>
    <input type="number" id="age" required>
    <span id="error"></span><br>
    <input type="button" value="Submit" onclick="processForm()">
</form>
```

#### Passed Example 2

The error message provided in the vicinity of the `input` element identifies the [input error](https://www.w3.org/TR/WCAG21/#dfn-input-error). Instructions are provided in help text and accessible description.

```html
<script>
    function processForm() {
        document.getElementById('error').innerText = "";
        var age = document.getElementById('age').value;
        console.log(isNaN(age));
        if (!age || isNaN(age)) {
            document.getElementById('error').innerText = "Age must be a number";
        } else if (age < 1) {
            document.getElementById('error').innerText = "Age must be positive";
        }
    }
</script>

<form>
    <label for="age">Age</label>
    <input type="number" id="age" aria-describedby="age_instructions">
    <span id="error"></span><br>
    <input type="button" value="Submit" onclick="processForm()">
</form>

<p>Form instructions:</p>
<p id="age_instructions">Enter age in years</p>
```

#### Passed Example 3

The error message provided in the vicinity of the `input` element identifies the [input error](https://www.w3.org/TR/WCAG21/#dfn-input-error). Instructions are provided in a tooltip.

```html
<html>

<head>

    <style>
        .form_tooltip:hover .tooltip {
            display: block;
        }

        .tooltip {
            display: none;
            background: #C8C8C8;
            margin-left: 28px;
            padding: 10px;
            position: absolute;
            z-index: 1000;
            width: 150px;
            height: 30px;
        }
    </style>

</head>

<body>

    <script>
        function processForm() {
            document.getElementById('error').innerText = "";
            var age = document.getElementById('age').value;
            console.log(isNaN(age));
            if (!age || isNaN(age)) {
                document.getElementById('error').innerText = "Age must be a number";
            } else if (age < 1) {
                document.getElementById('error').innerText = "Age must be positive";
            }
        }
    </script>

    <form>
        <div class="form_tooltip">
            <label for="age">Age</label>
            <input type="number" id="age">
            <p class="tooltip">Enter age in years</p>
        </div>
        <span id="error"></span><br>
        <input type="button" value="Submit" onclick="processForm()">
    </form>

</body>

</html>
```

### Failed

#### Failed Example 1

No error message is provided.


```html
<form>
    <label for="age">Age (years)</label>
    <input type="number" id="age" required>
    <span id="error"></span><br>
    <input type="button" value="Submit">
</form>

```

#### Failed Example 2

The error message does not identify the [input error](https://www.w3.org/TR/WCAG21/#dfn-input-error).

```html
<script>
    function processForm() {
        document.getElementById('error').innerText = "";
        var age = document.getElementById('age').value;
        console.log(isNaN(age));
        if (!age || isNaN(age) || age < 1) {
            document.getElementById('error').innerText = "Please fill the field correctly.";
        }
    }
</script>

<form>
    <label for="age">Age (years)</label>
    <input type="number" id="age" required>
    <span id="error"></span><br>
    <input type="button" value="Submit" onclick="processForm()">
</form>
```

#### Failed Example 3

The error message is not visible.

```html
<script>
    function processForm() {
        document.getElementById('error').innerText = "";
        var age = document.getElementById('age').value;
        console.log(isNaN(age));
        if (!age || isNaN(age)) {
            document.getElementById('error').innerText = "Age must be a number";
        } else if (age < 1) {
            document.getElementById('error').innerText = "Age must be positive";
        }
    }
</script>

<form>
    <label for="age">Age (years)</label>
    <input type="number" id="age" required>
    <span id="error" style="position: absolute; top: -9999px; left: -9999px;"></span><br>
    <input type="button" value="Submit" onclick="processForm()">
</form>
```

#### Failed Example 4

The error message is not included in the accessibility tree.

```html
<script>
    function processForm() {
        document.getElementById('error').innerText = "";
        var age = document.getElementById('age').value;
        console.log(isNaN(age));
        if (!age || isNaN(age)) {
            document.getElementById('error').innerText = "Age must be a number";
        } else if (age < 1) {
            document.getElementById('error').innerText = "Age must be positive";
        }
    }
</script>

<form>
    <label for="age">Age (years)</label>
    <input type="number" id="age" required>
    <span id="error" aria-hidden="true"></span><br>
    <input type="button" value="Submit" onclick="processForm()">
</form>
```

### Inapplicable

#### Inapplicable Example 1

The `input` element is not inside a `form` element

```html
<input type="text">
```