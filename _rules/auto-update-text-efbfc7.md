---
id: efbfc7
name: Text content that updates automatically can be paused, stopped or hidden
rule_type: atomic
description: |
  This rule checks that there are mechanisms to pause, stop or hide the auto-updating of text content.
accessibility_requirements: # Remove whatever is not applicable
  wcag20:2.2.2: # Pause, Stop, Hide (A)
    forConformance: true
    failed: not satisfied
    passed: further testing needed
    inapplicable: further testing needed
input_aspects:
  - DOM Tree
  - CSS Styling
acknowledgements:
  authors:
    - Carlos Duarte
---

## Applicability

The rule applies to any [visible][] [HTML element][] in an [HTML document][] if:

- the `innerText` property of the [element][html element] changes without the user [activating][activate] or [focusing][focus] any [element][html element] in the same [HTML document][];
- the [element][html element] does not have [children][child] whose `innerText` property is also changed;
- the change happens after the [readiness][document readiness] of the [HTML document][] the [element][html element] belongs to is equal to "complete";
- it is not the only [content][] in the [HTML document][].

## Expectation

For the test target a [user interface component][] is provided to pause, stop or hide the change of the [text content][].

**Note**: If there is more than one test target, a single [user interface component][] may be used to pause, stop or hide changing all test targets.

## Assumptions

This rule assumes that the auto-updating of the content is not [essential][], which is listed as valid exception to [Success Criterion 2.2.2: Pause, Stop, Hide][sc 2.2.2]. When the auto-updating of content is [essential][] this rule may produce incorrect results.

## Accessibility Support

_There are no major accessibility support issues known for this rule._

## Background

- [Understanding Success Criterion 2.2.2: Pause, Stop, Hide][sc 2.2.2]
- [G186: Using a control in the Web page that stops moving, blinking, or auto-updating content][g186]
- [F16: Failure of Success Criterion 2.2.2 due to including scrolling content where movement is not essential to the activity without also including a mechanism to pause and restart the content][f16]

## Test Cases

### Passed

#### Passed Example 1

The text content automatically updates after the page completes loading. A button is available to stop the automatic updates.

```html
<body onload="startUpdates()">
	<p>Random number: <span id="target">1</span></p>
	<input type="button" onclick="stopUpdates()" value="Stop updates" />

	<p>
		The W3C Web Accessibility Initiative (WAI) develops standards and support materials to help you understand and
		implement accessibility.
	</p>

	<script type="text/javascript" src="/test-assets/efbfc7/script.js"></script>
</body>
```

#### Passed Example 2

The text content automatically updates after the page completes loading. A button is available to pause and resume the automatic updates.

```html
<body onload="startUpdates()">
	<p>Random number: <span id="target">1</span></p>
	<input type="button" id="control" onclick="toggleUpdates()" value="Pause updates" />

	<p>
		The W3C Web Accessibility Initiative (WAI) develops standards and support materials to help you understand and
		implement accessibility.
	</p>

	<script type="text/javascript" src="/test-assets/efbfc7/script.js"></script>
</body>
```

#### Passed Example 3

The text content automatically updates after the page completes loading. A button is available to hide the automatically updating content.

```html
<body onload="startUpdates()">
	<p>Random number: <span id="target">1</span></p>
	<input type="button" onclick="hide()" value="Hide updates" />

	<p>
		The W3C Web Accessibility Initiative (WAI) develops standards and support materials to help you understand and
		implement accessibility.
	</p>

	<script type="text/javascript" src="/test-assets/efbfc7/script.js"></script>
</body>
```

### Failed

#### Failed Example 1

The text content automatically updates after the page completes loading. There is no component to stop or pause the automatic updates or to hide the updating content.

```html
<body onload="startUpdates()">
	<p>Random number: <span id="target">1</span></p>

	<p>
		The W3C Web Accessibility Initiative (WAI) develops standards and support materials to help you understand and
		implement accessibility.
	</p>

	<script type="text/javascript" src="/test-assets/efbfc7/script.js"></script>
</body>
```

### Inapplicable

#### Inapplicable Example 1

The text content automatically updates after the page completes loading but it is not visible.

```html
<body onload="startUpdates()">
	<p style="display: none">Random number: <span id="target">1</span></p>

	<p>
		The W3C Web Accessibility Initiative (WAI) develops standards and support materials to help you understand and
		implement accessibility.
	</p>

	<script type="text/javascript" src="/test-assets/efbfc7/script.js"></script>
</body>
```

#### Inapplicable Example 2

The text content automatically updates but only as a result of the user activating an element on the page.

```html
<body>
	<p>Random number: <span id="target">1</span></p>
	<input type="button" id="control" onclick="startUpdates()" value="Start updates" />

	<p>
		The W3C Web Accessibility Initiative (WAI) develops standards and support materials to help you understand and
		implement accessibility.
	</p>

	<script type="text/javascript" src="/test-assets/efbfc7/script.js"></script>
</body>
```

#### Inapplicable Example 3

The automatically updating text content is the only content in the document.

```html
<body onload="startUpdates()">
	<span id="target">1</span>

	<script type="text/javascript" src="/test-assets/efbfc7/script.js"></script>
</body>
```

[activate]: https://html.spec.whatwg.org/#activation
[child]: https://dom.spec.whatwg.org/#concept-tree-child
[content]: https://www.w3.org/TR/WCAG21/#dfn-content
[document readiness]: https://www.w3.org/TR/html53/dom.html#current-document-readiness
[essential]: https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html#dfn-essential
[focus]: https://html.spec.whatwg.org/#focus
[f16]: https://www.w3.org/WAI/WCAG21/Techniques/failures/F16
[g186]: https://www.w3.org/WAI/WCAG21/Techniques/general/G186
[html document]: https://dom.spec.whatwg.org/#html-document
[html element]: https://html.spec.whatwg.org/multipage/dom.html#htmlelement
[sc 2.2.2]: https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide
[text content]: #text-content 'Definition of text content'
[user interface component]: https://www.w3.org/TR/WCAG21/#dfn-user-interface-components
[visible]: #visible 'Definition of visible'
