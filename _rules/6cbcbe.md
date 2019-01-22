---
name: Links with identical accessible names serve equivalent purpose
test_type: atomic

description: |
  This rule checks that identical accessible names are only used for links that serve an equivalent purpose

success_criterion: 
- 2.4.9 # Link Purpose (Link Only)

test_aspects:
- DOM Tree
- CSS Styling

authors:
- Anne Thyme Nørregaard
---

## Test Procedure

### Applicability

This rule applies to any two or more HTML or SVG elements that have the [semantic role](#semantic-role) of link, are [included in the accessibility tree](#included-in-the-accessibility-tree) and that have the same [non-empty](#non-empty) [accessible name](#accessible-name).

### Expectation

When activated, the links in each set of target elements resolve to resources that fulfill an [equivalent purpose](#equivalent-purpose) in relation to the [accessible names](#accessible-name) of the link.

**Note:** Resolving the links includes potential redirects.

## Assumptions

* This rule assumes that the purpose of the links for links with identical names would not be ambiguous to users in general.

## Accessibility support

There are no major accessibility support issues known for this rule.

## Background

- [Understanding Success Criterion 2.4.9: Link Purpose (Link Only)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-link-only.html)
- [URL parsing](#https://www.w3.org/TR/html52/infrastructure.html#parsing-urls)

## Test Cases

### Passed

#### Passed example 1

Identical link text leads to identical URLs:

```html
<a href="/test-assets/link-purpose/index.html">Link text</a>
<a href="/test-assets/link-purpose/index.html">Link text</a>
```

#### Passed example 2

Links resolves to same page after redirect:

```html
<a href="/test-assets/link-purpose/index.html">Link text</a>
<a href="/test-assets/link-purpose/redirect.html">Link text</a>
```

#### Passed example 3

Identical pages are located on different URLs:

```html
<a href="/test-assets/link-purpose/index.html">Link text</a>
<a href="/test-assets/link-purpose/index-copy.html">Link text</a>
```

#### Passed example 4

Same link text used for links going to pages where the content section is the same, but where the navigation options (bread crumbs and local sub menus) differ due to different placement in navigation hierarchy:

```html
<a href="/test-assets/link-purpose/about/contact.html">Link text</a>
<a href="/test-assets/link-purpose/careers/contact.html">Link text</a>
```

#### Passed example 5

URLs differ due to trailing slashes:

```html
<a href="/test-assets/link-purpose/link-purpose">Link text</a> 
<a href="/test-assets/link-purpose/link-purpose/">Link text</a>
```

#### Passed example 6

Pages contain different amounts of information and/or differently worded information, but fulfils same purpose in relation to the link:

```html
<a href="/test-assets/link-purpose/page1.html">Link text</a>
<a href="/test-assets/link-purpose/page2.html">Link text</a>
```

#### Passed example 7

Has the same content but use different layouts:

```html
<a href="/test-assets/link-purpose/page1.html">Link text</a>
<a href="/test-assets/link-purpose/page3.html">Link text</a>
```

#### Passed example 8

Links created via scripting with explicit role of link: 

```html
<span role="link"
   onclick="location='/test-assets/link-purpose/link-purpose/index.html'">
Link text
</span>

<span role="link"
   onclick="location='/test-assets/link-purpose/link-purpose/index.html'">
Link text
</span>
```

### Failed

#### Failed example 1

Same link text used for links going to different resources:

```html
<a href="http://facebook.com">Follow us</a> 
<a href="http://twitter.com">Follow us</a>
```

#### Failed example 2

Same link text used for links going to web pages with same name, but with different information:

```html
<a href="/test-assets/link-purpose/social-sciences/contact.html">Contact us</a> 
<a href="/test-assets/link-purpose/humanities/contact.html">Contact us</a>
```

#### Failed example 3

Links created via scripting with explicit role of link: 

```html
<span role="link"
   onclick="location='/test-assets/link-purpose/link-purpose/page1.html'">
Link text
</span>

<span role="link"
   onclick="location='/test-assets/link-purpose/link-purpose/contact.html'">
Link text
</span>
```

### Inapplicable 

#### Inapplicable example 1

´a´ and ´area´ elements without ´href´ attribute:

```html
<a>Link text</a>
<area aria-label="Link text">
```

#### Inapplicable example 2

No identical link texts:

```html
<a href="/test-assets/link-purpose">Link text 1</a>
<a href="/test-assets/link-purpose">Link text 2</a>
```

#### Inapplicable example 3

Link is not exposed to assistive technologies;

```html
<a href="/test-assets/link-purpose" aria-hidden="true">Link text 1</a>
<a href="/test-assets/link-purpose">Link text 2</a>
```

#### Inapplicable example 4

Links created via scripting, but doesn't have semantic role of link:

```html
<span
   onclick="location='/test-assets/link-purpose/link-purpose/page1.html'">
Link text
</span>

<span
   onclick="location='/test-assets/link-purpose/link-purpose/contact.html'">
Link text
</span>
```