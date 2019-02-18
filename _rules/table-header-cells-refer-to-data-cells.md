---
name: All table header cells refer to data cells

test_type: atomic

description: |
  This rule checks that each table header in a data table refers to data cells.

test_aspects:
- DOM Tree

authors:
- Jey Nandakumar
- Audrey Maniez
---

## Test Procedure

### Applicability

This rule applies to any element with [semantic role](#semantic-role) of `columnheader` or `rowheader` within the `table` element that is either [visible](#visible) or [included in the accessibility tree](#included-in-the-accessibility-tree).

### Expectation
- Each target element with the `headers` attribute refers to other `cells` of the same `table`.

Each target element refers to data `cells` of the same `table`.

## Assumptions

*There are currently no assumptions*

## Accessibility support

*There are no major accessibility support issues known for this rule.*

## Background

- [Understanding Success Criterion 1.3.1: Information and relationships](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
- [H43: Using id and headers attributes to associate data cells with header cells in data tables](https://www.w3.org/WAI/WCAG21/Techniques/html/H43)


## Test Cases

### Passed

#### Passed example 1

The `columnheader` refers to `cells` within the same `table`.

```html
<table>
  <thead>	
    <tr>
      <th id="header1">Projects</th>
      <th id="header2">Exams</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2" headers="header1 header2">15%</td>
    </tr>
  </tbody>
</table>
```

#### Passed example 2

The `columnheader` refers to `cells` within the same `table`.

```html
<table>
  <tr> 
    <td headers="header1">
      Projects
    </td>
    <th id="header1">
      Projects
    </th> 
  </tr>
</table>
```

#### Passed example 3

The `columnheader` refers to `cells` within the same `table`.

```html
<table>
  <tr> 
    <td aria-labelledby="header1">
      Description
    </td>
    <th id="header1">
      Description
    </th> 
  </tr>
</table>
```


### Failed

#### Failed example 1

The `columnheader` do not refer to `cells` within the `table`.

```html
<table>
  <tr>
    <th id="header1">Projects</th>
    <th id="header2">Exams</th>
  </tr>
  <tr>
    <td colspan="2">15%</td>
  </tr>
</table>
```


### Inapplicable

#### Inapplicable example 1

The rule only applies only to `table` element.

```html
<div role="table">
 <div role="row">
  <div class="columnheader" id="header1">Projects</div>
  <div class="columnheader" id="header2">Exams</div>
 </div>
 <div role="row">
  <div role="cell" headers="header2">15%</div>
  <div role="cell" headers="header1">15%</div>
 </div>
</div>
```

#### Inapplicable example 2

The rule only applies to `table` element that is included in the accessibility tree, `table` is marked as `role=presentation`.

```html
<table role="presentation">
  <tr> <th>Time</th> </tr>
  <tr> <th>Date</th> </tr>
</table>
```


#### Inapplicable example 3

The rule only applies to `table` element that is included in the accessibility tree, `table` is marked as `aria-hidden=true`.

```html
<table aria-hidden="true">
  <tr> <th>Time</th> </tr>
  <tr> <th>Date</th> </tr>
</table>
```