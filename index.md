---
layout: default
---

<h2 id="toc">Inhaltsverzeichnis</h2>

<div markdown="1">
### [HTML](#html)

- [HTML Syntax](#html-syntax)
- [HTML5 doctype](#html5-doctype)
- [Language Attribut](#language-attribute)
- [IE Kompatibilitätsmodus](#ie-compatibility-mode)
- [Zeichenencodierung](#character-encoding)
- [CSS und JavaScript includes](#css-and-javascript-includes)
- [Zweckmäßigkeit vor Ordnung](#practicality-over-purity)
- [Attribut-Reihenfolge](#attribute-order)
- [Boolean Attribute](#boolean-attributes)
- [Markup reduzieren](#reduce-markup)
- [Editor Einstellungen](#editor-preferences)
</div>

<div markdown="1">
### [CSS](#css)

- [CSS Syntax](#css-syntax)
- [Reihenfolge der Deklarationen](#declaration-order)
- [Farben](#colors)
- [Logische Eigenschaften](#logical-properties)
- [Vermeide @import](#avoid-imports)
- [Media Query Platzierung](#media-query-placement)
- [Einzelne Deklarationen](#single-declarations)
- [Kurzschreibweisen](#shorthand-notation)
- [Verschachtelungen in Preprozessoren](#nesting-in-preprocessors)
- [Operatoren in Preporzessoren](#operators-in-preprocessors)
- [Kommentare](#comments)
- [Klassennamen](#class-names)
- [Selektoren](#selectors)
- [Child und nachkommende Selektoren](#child-and-descendant-selectors)
- [Organisation](#organization)
</div>

## Die goldene Regel

Setze diese oder deine eigenen, vereinbarten, Leitlinien stets durch. Ob klein oder groß, weise darauf hin, was falsch ist. Für Ergänzungen oder Beiträge zu diesem Code-Leitfaden, [öffnen bitte ein Issue auf GitHub](https://github.com/mdo/code-guide/issues/new) (auf Englisch).

> Jede einzelne Code-Zeoile sollte so aussehen, als wäre sie von einer einzelnen Person geschrieben worden sein, unabhänig von der Anzahl der Mitwirkenden.

## HTML

<div markdown="1">
### Syntax
{: #html-syntax }

- Tags, einschließlich des doctype, sollten nicht groß geschrieben werden.
- Benutze "Soft Tabs" mit zwei Leerzeichen-nur so kann garantiert werden, dass dein Code in jeder Umgebung gleich dargestellt wird.
- Verschachtelte Elemente sollten einmal eingerückt werden (mit zwei Leerzeichen).
- Benutze immer doppelte Anführungszeichen für Attribute, niemals einzelne.
- Benutze keinen abschließenden Schrägstrich in Selbstschließenden Elementen-Laut [HTML5 Spezifikation](https://html.spec.whatwg.org/multipage/syntax.html#syntax-start-tag) sind diese optional.
- Lasse keine optionalen schließende Tags (z.B. `</li>` oder `</body>`) weg.
</div>

```html
<!doctype html>
<html>
  <head>
    <title>Seitentitel</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hallo-welt">Hallo Welt!</h1>
  </body>
</html>
```

<div markdown="1">
### HTML5 doctype

Erzwinge den [Standard Modus](https://developer.mozilla.org/en-US/docs/Web/HTML/Quirks_Mode_and_Standards_Mode) und eine einheitlichere Darstellung in jedem Brwoser mit diesem einfachem doctype am Anfang einer jeden HTML Seite. Halte das doctype-tag, in Übereinstimmung mit der vorgeschlagenen Syntax, in Kleinbuchstaben.
</div>

```html
<!doctype html>
<html>
  <head>
    <!-- ... -->
  </head>
  <body>
    <!-- ... -->
  </body>
</html>
```

<div markdown="1">
### Language Attribut

From the HTML5 spec:
Aus der HTML5 Spezifikation: 

> Die Autoren werden aufgefordert, ein lang-Attribut auf dem html-Root-Element anzugeben, das die Sprache des Dokuments angibt. Dies hilft Sprachsynthesewerkzeugen bei der Bestimmung der zu verwendenden Aussprache, Übersetzungswerkzeugen bei der Bestimmung der zu verwendenden Regeln und so weiter.

Mehr Informationen über das `lang`-Attribut sind [in der Spezifikation](https://html.spec.whatwg.org/multipage/semantics.html#the-html-element) zu finden. Auf der Seite der <abbr title="Internet Assigned Numbers Authority">IANA</abbr> st eine [Liste von Sprachcodes](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) zu finden.
</div>

```html
<html lang="de">
  <!-- ... -->
</html>
```

<div markdown="1">
### IE Kompatibilitätsmodus 

Heutzutage ist es nicht mehr nötig, das Internet Explorer-Dokumentenkompatibilitäts-Tag "<meta>" einzufügen, es sei denn, Sie benötigen Unterstützung für IE10 und ältere Versionen. Das Tag wurde im IE11 gestrichen und wird in Microsoft Edge (ob Legacy oder nicht) nicht verwendet.
Es ist heutzutage nicht mehr nötig, das Internet Explorer Dokumentenkompatibilitäts-Tag `<meta>` einzufügen, außer es wird Unterstützung für den IE10 oder älter benötigt. Das Tag wurde im IE11 und in Microsoft Edge (egal ob Legacy oder neuer) nicht verwendet.

For more information, [read this awesome Stack Overflow article](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do).
</div>

```html
<!-- IE10 and below only -->
<meta http-equiv="x-ua-compatible" content="ie=edge">
```

<div markdown="1">
### Zeichenencodierung

Ensure proper content rendering by declaring an explicit character encoding. This also allows you to use regular characters instead of their HTML entities, like `—` instead of `&emdash;`, provided their encoding matches that of the document. For some reserved XML characters—like ampersand, non-breaking spaces, less/greater than, and quotes—you may still need to use the HTML character entities.

Stelle die korrekte Anzeige von Inhalten durch die Angabe einer explizite Zeichenkodierung sicher. Dadurch können  auch reguläre Zeichen anstelle ihrer HTML-Entitäten verwendet werden, z. B. `-` anstelle von `&emdash;`, sofern ihre Kodierung mit der des Dokuments übereinstimmt. Für einige reservierte XML-Zeichen wie das kaufmännische Und-Zeichen, nicht umbrechende Leerzeichen, kleiner/größer als und Anführungszeichen müssen Sie möglicherweise immer noch die HTML-Zeichenentitäten verwenden.

UTF-8 is the recommended encoding.
</div>

```html
<head>
  <meta charset="utf-8">
</head>
<body>
  <p>Benuze einen em dash wie hier-du brauchst keine HTML-Entität.</p>
</body>
```

<div markdown="1">
### CSS und JavaScript includes

Nach der HTML5 Spezifikation muss typischerweise kein `type` angegeben werden, wenn CSS und JavaScript Dateien eingebunden werden, da `text/css` und `text/javascript` respektive deren Standards sind.

#### HTML5 Spezifikationen Verweise

- [Benutzung von link](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
- [Benutzung von style](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
- [Benutzung von script](https://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)
</div>

```html
<!-- Externes CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- CSS im Dokument -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

<div markdown="1">
### Zweckmäßigkeit vor Ordnung

Bemühe dich um die Einhaltung der HTML-Standards und der Semantik, aber nicht auf Kosten der Praktikabilität. Verwende, wann immer es möglich ist, so wenig Markup wie möglich und gestalte es so unkompliziert wie möglich.
</div>

```html
<!-- Gut -->
<button>...</button>

<!-- Nicht gut -->
<div class="btn" onClick="...">...</div>
```

<div markdown="1">
### Attribut-Reihenfolge

HTML Attribute sollten in dieser spezifischen Reihenfolge angeordnet sein, um das Lesen des Codes einfacher zu machen.

- `class`
- `id`, `name`
- `data-*`
- `src`, `for`, `type`, `href`, `value`
- `title`, `alt`
- `role`, `aria-*`
- `tabindex`
- `style`

Attribute, die zumeist zum Identifzieren von Elementen genutzen werden, sollten zuerst kommen—`class`, `id`, `name`, und `data` Attribute. An zweiter Stelle stehen verschiedene Attribute, die nur für bestimmte Elemente gelten, gefolgt von Attributen, die sich auf die Zugänglichkeit und das Styling beziehen.
</div>

```html
<a class="..." id="..." data-toggle="modal" href="#">
  Beispiel Link
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

<div markdown="1">
### Boolean Attribute

Ein "boolean" Attribut benötigt keinen deklarierten Wert. Bei XHTML musste ein Wert angegeben werden, aber bei HTML5 ist dies nicht erforderlich.

Mehr Informationen gibt es in der [WhatWG Sektion über "boolean attributes" (Englisch)](https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes)

> Das Vorhandensein eines Boolean Attributs in einem Element steht für den wahren Wert, das Fehlen des Attributs für den falschen Wert.

Wenn du den Wert des Attributs angeben <em>musst</em>, dies aber **nicht erforderlich ist**, befolge diese WhatWG-Richtlinie:

> Wenn das Attribut vorhanden ist, muss sein Wert entweder die leere Zeichenkette oder [...] der kanonische Name des Attributs sein, ohne führende oder nachfolgende Leerzeichen.

Kurz: **Füge keinen Wert hinzu**.
</div>

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

<div markdown="1">
### Markup reduzieren

Wann immer es möglich ist, sollten beim Schreiben von HTML, überflüssige, übergeordnete Elemente vermieden werden. Dies erfordert oft Iteration und Refactoring, führt aber zu weniger HTML.
</div>

```html
<!-- Nicht so gut -->
<span class="avatar">
  <img src="...">
</span>

<!-- Besser -->
<img class="avatar" src="...">
```

<div markdown="1">
### Editor Einstellungen

Stelle deinen Code-Editor so ein, um unsaubere Diffs und häufig vorkommende Inkonsistenzen im Code zu vermeiden:

- Benutze "Soft-Tabs" (auf 2 Leerzeichen gesetzt).
- Nachfolgende Leerzeichen beim Speichern abschneiden.
- Setze die Encodierung auf UTF-8.
- Füge eine neue Zeile am Ende eines Dokuments hinzu.

Ziehe in Erwägung, diese Einstellungen in der `.editorconfig`-Datei deines Projekts zu dokumentieren. Sie dir zum Beispiel [die Konfiguration von Bootstrap](https://github.com/twbs/bootstrap/blob/main/.editorconfig) an. Erfahre hier mehr [über EditorConfig](https://editorconfig.org).
</div>

## CSS

<div markdown="1">
### Syntax
{: #css-syntax }

- Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment.
- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after `:` for each declaration.
- Each declaration should appear on its own line for more accurate error reporting.
- End all declarations with a semi-colon. The last declaration's is optional, but your code is more error prone without it.
- Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
- Use space-separated values for color properties (e.g., `color: rgb(0 0 0 / .5)`). [See the Colors section for more information.](#colors)
- Don't prefix property values or color parameters with a leading zero (e.g., `.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
- Lowercase all hex values, e.g., `#fff`. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
- Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.
- Quote attribute values in selectors, e.g., `input[type="text"]`. [They’re only optional in some cases](https://mathiasbynens.be/notes/unquoted-attribute-values#css), and it’s a good practice for consistency.
- Avoid specifying units for zero values, e.g., `margin: 0;` instead of `margin: 0px;`.

Questions on the terms used here? See the [syntax section of the Cascading Style Sheets article](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax) on Wikipedia.
</div>

```scss
// Bad CSS
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

// Good CSS
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgb(0 0 0 / .5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

<div markdown="1">
### Declaration order

Property declarations should be grouped together in the following order:

1. Positioning
2. Box model
3. Typographic
4. Visual
5. Misc

Positioning comes first because it can remove an element from the normal document flow and override box model related styles. The box model—whether it's flex, float, grid, or table—follows as it dictates a component's dimensions, placement, and alignment. Everything else takes place _inside_ the component or without impacting the previous two sections, and thus they come last.

While `border` is part of the box model, most systems globally reset the [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) to `border-box` so that `border-width` doesn't affect overall dimensions. This, combined with keeping `border` near `border-radius`, is why it's under the Visual section instead.

Preprocessor mixins and functions should appear wherever most appropriate. For example, a `border-top-radius()` mixin would go in place of `border-radius` properties, while a `responsive-font-size()` function would go in place of `font-size` properties.

For a complete list of properties and their order, please see the [property order for Stylelint](https://github.com/stormwarning/stylelint-config-recess-order) used by [Bootstrap](https://getbootstrap.com).
</div>

```scss
.declaration-order {
  // Positioning
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  // Box model
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;

  // Typography
  font: normal 14px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
  text-decoration: underline;

  // Visual
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  // Misc
  opacity: 1;
}
```

<div markdown="1">
### Logical properties

Logical properties are alternatives to directional and dimensonal properties based on abstract terms like *block* and *inline*. By default, block refers to the vertical direction (top and bottom) while inline refers to the horizontal direction (right and left). You can begin to use these values in your CSS in all modern, evergreen browsers.

**Why use logical properties?** Not every language flows left-ro-right like English, so the [writing mode](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode) needs to be flexible. With logical properties, you can easily support languages that can be written horizontally or vertically (like Chinese, Japanese, and Korean). Plus, they're usually shorter and simpler to write.

**Additional reading:**

- [CSS Logical Properties and Values – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties)
- [CSS Logical Properties and Values — CSS Tricks](https://css-tricks.com/css-logical-properties-and-values/)
- [CSS Writing Modes – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Writing_Modes)
</div>

```scss
// Without logical properties
.element {
  margin-right: auto;
  margin-left: auto;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
}

// With logical properties
.element {
  margin-inline: auto;
  border-block: 1px solid #eee;
}
```

<div markdown="1">
### Colors

With the support of [CSS Color Levels 4](https://www.w3.org/TR/css-color-4/) [in all major browsers](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgb#space-separated_values), `rgba()` and `hsla()` are now aliases for `rgb()` and `hsl()`, meaning you can modify alpha values in `rgb()` and `hsl()`. Along with this comes support for new space-separated syntax for color values. For compability with future CSS color functions, use this new syntax.

Regardless of your color values and syntax, always ensure your color choices meet [WCAG minimum contrast ratios](https://webaim.org/articles/contrast/) (4.5:1 for 16px and smaller, 3:1 for larger).

**Additional reading:**

- [Smashing Magazine - A Guide To Modern CSS Colors](https://www.smashingmagazine.com/2021/11/guide-modern-css-colors/)
- [`rgb()` - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgb)
</div>

```css
.element {
  color: rgb(255 255 255 / .65);
  background-color: rgb(0 0 0 / .95);
}
```

<div markdown="1">
### Avoid `@import`s

Compared to `<link>`s, `@import` is slower, adds extra page requests, and can cause other unforeseen problems. Avoid them and instead opt for an alternate approach:

- Use multiple `<link>`elements
- Compile your CSS with a preprocessor like [Sass](https://sass-lang.com/) or [Less](https://lesscss.org/) into a single file
- Concatenate your CSS files with features provided in Rails, Jekyll, and other environments

For more information, [read this article by Steve Souders](https://www.stevesouders.com/blog/2009/04/09/dont-use-import/).
</div>

```html
<!-- Use link elements -->
<link rel="stylesheet" href="core.css">

<!-- Avoid @imports -->
<style>
  @import url("more.css");
</style>
```

<div markdown="1">
### Media query placement

Place media queries as close to their relevant rule sets whenever possible. Don't bundle them all in a separate stylesheet or at the end of the document. Doing so only makes it easier for folks to miss them in the future. Here's a typical setup.
</div>

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (min-width: 480px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

<div markdown="1">
### Single declarations

In instances where a rule set includes **only one declaration**, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines.

The key factor here is error detection—e.g., a CSS validator stating you have a syntax error on Line 183. With a single declaration, there's no missing it. With multiple declarations, separate lines is a must for your sanity.
</div>

```scss
// Single declarations on one line
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

// Multiple declarations, one per line
.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url("../img/sprite.png");
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
```

<div markdown="1">
### Shorthand notation

Limit shorthand declaration usage to instances where you must explicitly set all available values. Frequently overused shorthand properties include:

- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

Usually we don't need to set all the values a shorthand property represents. For example, HTML headings only set top and bottom margin, so when necessary, only override those two values. A `0` value implies an override of either a browser default or previously specified value.

Excessive use of shorthand properties leads to sloppier code with unnecessary overrides and unintended side effects.

The Mozilla Developer Network has a great article on [shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) for those unfamiliar with notation and behavior.
</div>

```scss
// Bad example
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

// Good example
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

<div markdown="1">
### Nesting in preprocessors

Avoid unnecessary nesting in preprocessors whenever possible—keep it simple and avoid reverse nesting. Consider nesting only if you must scope styles to a parent and if there are multiple elements to be nested.

**Additional reading:**

- <a href="https://markdotto.com/2015/07/20/css-nesting/">Nesting in Sass and Less</a>
</div>

```scss
// Without nesting
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// With nesting
.table > thead > tr {
  > th { … }
  > td { … }
}
```

<div markdown="1">
### Operators in preprocessors

For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.
</div>

```scss
// Bad example
.element {
  margin: 10px 0 @variable*2 10px;
}

// Good example
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```

<div markdown="1">
### Comments

Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Use the `//` syntax when writing CSS with preprocessors. When shipping CSS to production, remove all comments.

Be sure to write in complete sentences for larger comments and succinct phrases for general notes.
</div>

```scss
// Bad example
// Modal header
.modal-header {
  ...
}

// Good example
// Wrapping element for .modal-title and .modal-close
.modal-header {
  ...
}
```

<div markdown="1">
### Class names

- Keep classes lowercase and use dashes (not underscores or camelCase). Dashes serve as natural breaks in related class (e.g., `.btn` and `.btn-danger`).
- Avoid excessive and arbitrary shorthand notation. `.btn` is useful for _button_, but `.s` doesn't mean anything.
- Keep classes as short and succinct as possible.
- Use meaningful names; use structural or purposeful names over presentational.
- Prefix classes based on the closest parent or base class.
- Use `.js-*` classes to denote behavior (as opposed to style), but keep these classes out of your CSS.

It's also useful to apply many of these same rules when creating custom properties and preprocessor variable names.
</div>

```scss
// Bad example
.t { ... }
.red { ... }
.header { ... }

// Good example
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

<div markdown="1">
### Selectors

- Use classes over generic element tags for more explicit and reliable styling that isn't dependent on your markup.
- Avoid using several attribute selectors (e.g., `[class^="..."]`) on commonly occuring components. Browser performance is known to be impacted by these.
- Keep selectors short and strive to limit the number of elements in each selector to three.
- Scope classes to the closest parent `only` when necessary (e.g., when not using prefixed classes).

**Additional reading:**

- [Scope CSS classes with prefixes](https://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
- [Stop the cascade](https://markdotto.com/2012/03/02/stop-the-cascade/)
</div>

```scss
// Bad example
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

// Good example
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

<div markdown="1">
### Child and descendant selectors

When necessary, it may be helpful to use [the child combinator (`>`)](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator) to limit the cascade of some styles in elements like `<table>`s that are often recursively nested. Use it to limit styles to the immediate children elements of a parent element to avoid unnecessary overrides later on.
</div>

```css
.custom-table > tbody > tr > td,
.custom-table > tbody > tr > th {
  /* ... */
}
```

<div markdown="1">
### Organization

- Organize sections of code by component.
- Develop a consistent commenting hierarchy.
- Use consistent white space to your advantage when separating sections of code for scanning larger documents.
- When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.
</div>

```scss
//
// Component section heading
//

.element { ... }


//
// Component section heading
//
// Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
//

.element { ... }

// Contextual sub-component or modifer
.element-heading { ... }
```
