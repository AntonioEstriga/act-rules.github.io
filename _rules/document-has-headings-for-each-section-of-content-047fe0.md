---
id: 047fe0
name: Document has headings for each section of content
rule_type: atomic
description: |
  This rule checks that each section of content starts with a heading
accessibility_requirements:
  wcag-technique:H69: # Providing heading elements at the beginning of each section of content
    forConformance: false
    failed: not satisfied
    passed: satisfied
    inapplicable: satisfied
input_aspects:
  - DOM Tree
  - CSS styling
acknowledgments:
  authors:
    - Jean-Yves Moyen
  assets:
    - _The Three Kingdoms_ by Yu Sumei (Tuttle publishing, May 2014, ISBN 9780804843935)
    - Image from a Ming Dynasty edition of the Romance of the Three Kingdoms, original kept in the library holdings of Peking University.
---

**Note to reviewers:** I am not sure whether this rule maps to [2.4.10: Section Headings](https://www.w3.org/WAI/WCAG21/Understanding/section-headings.html). Because the SC says that "'Heading' is used in its general sense and includes titles and other ways to add a heading to different types of content." So I am not sure that not having element with a role of `heading` at the start of a section of content is enough to fail the SC. What is your opinion?

## Applicability

This rule applies to any [HTML web page][].

## Expectations

For each [section of content][] in the test target, the first node in the [flat tree][] which is inside this [section of content][] and has a non-empty [accessible name][]:

- has a [semantic role][] of `heading`; and
- is [visible][]; and
- is [included in the accessibility tree][].

**Note** Neither this rule, nor technique [H69: Providing heading elements at the beginning of each section of content][tech h69], expects the heading to accurately describe its corresponding section. However, having non descriptive headings fails [Success Criterion 2.4.6: Headings and Labels](https://www.w3.org/TR/WCAG21/#headings-and-labels)

**Note:** Neither this rule, nor technique [H69: Providing heading elements at the beginning of each section of content][tech h69], expects that headings are correctly nested without skipping level. It is nonetheless recommended to nest headings hierarchically without skipping levels.

## Assumptions

This rule assumes that headings used to pass technique [H69: Providing heading elements at the beginning of each section of content][tech h69] have to be [visible][] and [included in the accessibility tree][] in order to be beneficial to all users whether they are using assistive technologies or not.

## Accessibility Support

Having headings is sufficient to pass [Success Criterion 2.4.1: Bypass blocks][sc241]. However, if headings are used for that goal, they will only benefit users who can actually navigate from heading to heading (such a functionality can be provided by browsers, browsers plugins, screen readers or other assistive technologies). Users without any possibility for heading navigation will be left without way of bypassing blocks of repeated content and will still experience accessibility issues. Therefore, it is recommended to provide other ways of bypassing blocks.

**Note to reviewers**: In its current state, the definition of [section of content][] would include, e.g. an advertising sidebar as a specific section of content. However, it is not clear that the lack of heading on it would be a breach of H69 or SC 2.4.1… Idea?

## Background

- [Understanding Success Criterion 2.4.1: Bypass Blocks][usc241]
- [H69: Providing heading elements at the beginning of each section of content][tech h69]
- [CSS Scoping (work in progress)](https://drafts.csswg.org/css-scoping/)

## Test Cases

**Note:** Unless specified otherwise, the [sections of content][section of content] of each document are defined by the [landmarks][landmark] (`main` and `nav` elements).

### Passed

#### Passed Example 1

This [document][] has one [section of content][] for the navigation links, and one for the actual text. Each starts with a `h1` heading.

**Note:** In this [document][], the [sections of content][section of content] are identified by the level 1 heading at their start.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<!-- Navigational section of content starts here -->
		<h1>Contents</h1>
		<!-- list of links to each chapter -->
		<!-- Navigational section of content ends here -->

		<!-- Main section of content starts here -->
		<h1>Three Heroes Swear Brotherhood at a Feast in the Peach Garden</h1>
		<p>
			Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span of
			time.
		</p>
		<!-- Main section of content ends here -->
	</body>
</html>
```

#### Passed Example 2

In this [document][], headings are not the first elements of each [section of content][], but they are the first with a non-empty [accessible name][]. The [accessible name][] of the second heading is inherited from its content.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<nav>
			<hr />
			<h1>Contents</h1>
			<!-- list of links to each chapter -->
		</nav>
		<main>
			<hr />
			<h1><span>Three Heroes Swear Brotherhood at a Feast in the Peach Garden</span></h1>
			<p>
				Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span
				of time.
			</p>
		</main>
	</body>
</html>
```

#### Passed Example 3

The image at the start of the second [section of content][] has an empty [accessible name][]. Thus, the first node with a non-empty [accessible name][] is the `h1` element and the rule passes.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<nav>
			<h1>Contents</h1>
			<!-- list of links to each chapter -->
		</nav>
		<main>
			<img src="../test-assets/bypass-blocks-cf77f2/peach-garden-oath.jpg" role="presentation" alt="" />
			<h1>Three Heroes Swear Brotherhood at a Feast in the Peach Garden</h1>
			<p>
				Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span
				of time.
			</p>
		</main>
	</body>
</html>
```

#### Passed Example 4

Each [section of content][] of this [document][] starts with a `div` element with a role of `heading`.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<nav>
			<div role="heading" aria-level="1">Contents</div>
			<!-- list of links to each chapter -->
		</nav>
		<main>
			<div role="heading" aria-level="1">Three Heroes Swear Brotherhood at a Feast in the Peach Garden</div>
			<p>
				Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span
				of time.
			</p>
		</main>
	</body>
</html>
```

#### Passed Example 5

This [document][] is using image as heading, the [accessible name][] of the image (given by the `alt` attribute) is also the [accessible name][] of the heading.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<nav>
			<h1>Contents</h1>
			<!-- list of links to each chapter -->
		</nav>
		<main>
			<h1>
				<img
					src="../test-assets/bypass-blocks-cf77f2/peach-garden-oath.jpg"
					alt="Three Heroes Swear Brotherhood at a Feast in the Peach Garden"
				/>
			</h1>
			<p>
				Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span
				of time.
			</p>
		</main>
	</body>
</html>
```

### Failed

#### Failed Example 1

For the main [section of content][], the first node with a non-empty [accessible name][] does not have a [semantic role][] of `heading`, even though it is styled to appear as one.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<nav>
			<h1>Contents</h1>
			<!-- list of links to each chapter -->
		</nav>
		<main>
			<strong style="font-size: 18pt">Three Heroes Swear Brotherhood at a Feast in the Peach Garden</strong>
			<p>
				Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span
				of time.
			</p>
		</main>
	</body>
</html>
```

#### Failed Example 2

The heading of the main [section of content][] is not [included in the accessibility tree][] because of the `aria-hidden` attribute.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<nav>
			<h1>Contents</h1>
			<!-- list of links to each chapter -->
		</nav>
		<main>
			<h1 aria-hidden="true">Three Heroes Swear Brotherhood at a Feast in the Peach Garden</h1>
			<p>
				Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span
				of time.
			</p>
		</main>
	</body>
</html>
```

#### Failed Example 3

The `h1` element at the start of the main [section of content][] has an empty [accessible name][] (because of the `aria-label` attribute). Therefore, the first node with a non-empty [accessible name][] is the `img` element which does not have a [semantic role][] of `heading`.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<nav>
			<h1>Contents</h1>
			<!-- list of links to each chapter -->
		</nav>
		<main>
			<h1 aria-label="">Three Heroes Swear Brotherhood at a Feast in the Peach Garden</h1>
			<img
				src="../test-assets/bypass-blocks-cf77f2/peach-garden-oath.jpg"
				alt="Three Heroes Swear Brotherhood at a Feast in the Peach Garden"
			/>
			<p>
				Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span
				of time.
			</p>
		</main>
	</body>
</html>
```

#### Failed Example 4

The `h1` element that starts the main [section of content][] is not [visible][] because it is off screen.

```html
<html>
	<head>
		<title>The Three Kingdoms, Chapter 1</title>
	</head>
	<body>
		<nav>
			<h1>Contents</h1>
			<!-- list of links to each chapter -->
		</nav>
		<main>
			<h1 style="position: absolute; top:-999px">Three Heroes Swear Brotherhood at a Feast in the Peach Garden</h1>
			<p>
				Unity succeeds division and division follows unity. One is bound to be replaced by the other after a long span
				of time.
			</p>
		</main>
	</body>
</html>
```

### Inapplicable

#### Inapplicable Example 1

This [document][] is not an [HTML web page][].

```svg
<svg xmlns="http://www.w3.org/2000/svg">
  <title>This is an SVG</title>
</svg>
```

[accessible name]: #accessible-name 'Definition of accessible name'
[document]: https://dom.spec.whatwg.org/#concept-document 'Definition of document'
[document element]: https://dom.spec.whatwg.org/#document-element 'Definition of document element'
[flat tree]: https://drafts.csswg.org/css-scoping/#flat-tree 'Definition of flat tree'
[included in the accessibility tree]: #included-in-the-accessibility-tree 'Definition of included in the accessibility tree'
[landmark]: https://www.w3.org/TR/wai-aria-1.1/#landmark_roles 'List of landmark roles'
[section of content]: #section-of-content 'Definition of section of content'
[semantic role]: #semantic-role 'Definition of semantic role'
[sc241]: https://www.w3.org/TR/WCAG21/#bypass-blocks 'Success Criterion 2.4.1: Bypass blocks'
[tech h69]: https://www.w3.org/WAI/WCAG21/Techniques/html/H69 'Technique H69: Providing heading elements at the beginning of each section of content'
[usc241]: https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html 'Understanding Success Criterion 2.4.1: Bypass blocks'
[visible]: #visible 'Definition of visible'
[html web page]: #web-page-html 'Definition of web page (HTML)'