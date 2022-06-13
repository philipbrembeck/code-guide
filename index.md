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
- [Verschachtelungen in Präprozessoren](#nesting-in-preprocessors)
- [Operatoren in Präprozessoren](#operators-in-preprocessors)
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

- Benutze "Soft-Tabs" mit zwei Leerzeichen–sie sind der einzige Weg, zu garantieren, dass der Code in jeder Umgebung gleich aussieht.
- Wenn Selektoren gruppiert werden, sollten sie in einer einzigen Zeile gehalten werden.
- Füge ein Leerzeichen vor der öffnenden Klammer eines Deklarationsblock ein, um die Lesbarkeit zu gewährleisten.
- Setze die schließende Klammer eines Deklarationsblock in eine neue Zeile.
- Setze ein Leerzeichen nach dem `:` für jede Deklaration.
- Jede Deklaration sollte für eine akkuratere Fehlerberichterstattung/Debugging in ihrer eigenen Zeile stehen.
- Beende alle Deklarationen mit einem Semikolon. Das Semikolon der letzten Deklaration eines Deklarationsblocks ist optional, aber dein Code ist ohne sie fehleranfälliger.
- Durch Kommas getrennte Eigenschaftswerte sollten nach jedem Komma ein Leerzeichen enthalen (z.B. `box-shadow`).
- Nutze durch Leerzeichen separierte Werte für Farbeigenschaften (z.B. `color: rgb(0 0 0 / .5)`). [Mehr dazu in der Farb-Sektion.](#colors)
- Stelle Eigenschaftswerten oder Farbparametern keine führende Null voran (z.B. `.5` anstelle von `0.5` und `-.5px` anstelle von `-0.5px`).
- Schreibe alle Hexadezimalwerte klein, z.B. `#fff`. Kleinbuchstaben sind beim Durchsuchen eines Dokuments viel leichter zu erkennen, da sie dazu tendieren, meist eine eindeutigere Form zu haben.
- Benutze Kurzformen von Hexadezimalwerten, wenn verfügbar, z.B. `#fff` anstelle von `#ffffff`.
- Setze Attributwerte in Selektoren in Anführungszeigen, z.B. `input[type="text"]`. [Sie sind nur in wenigen Fällen optional (Englisch)](https://mathiasbynens.be/notes/unquoted-attribute-values#css) und es ist eine gute Praxis für die Kohärenz im Code.
- Vermeide es, Einheiten für Nullwerte zu verwenden, z.B. `margin: 0;` anstelle von `margin: 0px;`.

Du hast Fragen zu den hier benutzen Begrifflichkeiten? Lies die [Syntax Sektion des Artikels über Cascading Style Sheets](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax) auf Wikipedia (Englisch).

</div>

```scss
// Schlechtes CSS
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

// Gutes CSS
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
### Reihenfolge der Deklarationen

Eigenschaftsdeklarationen sollten in der folgenden Reihenfolge gruppiert werden:

1. Positionierung
2. Box-Modell
3. Typografie 
4. Visuell
5. Sonstiges

Die Positionierung steht an erster Stelle, da sie ein Element aus dem normalen Dokumentfluss herausnehmen und Box-Modell-bezogene Stile außer Kraft setzen kann. Das Box-Modell-egal ob Flex, Float, Grid oder Table-folgt, da es die Abmessungen, die Platzierung und die Ausrichtung einer Komponente vorgibt. Alles andere geschieht _innerhalb_ der Komponente oder ohne Auswirkungen auf die beiden vorangegangenen Abschnitte und kommt daher zuletzt.

Während `border` Teil des Box-Modells ist, setzen die meisten Systeme die [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) global auf `border-box` zurück, sodass `border-width` keinen Einfluss auf die Gesamtabmessungen hat. Dies in Verbindung damit, dass `border` in der Nähe von `border-radius` liegen sollte, ist der Grund, warum es stattdessen unter dem Abschnitt "Visual" zu finden ist.

Präprozessoren Mixins und Funktionen sollten dort auftauchen, wo sie am geeignetsten erscheinen. Zum Beispiel würde ein `border-top-radius()` Mixin bei `border-radius`-Eigenschaften stehen, während eine `responsive-font-size()`-Funktion anstelle von `font-size`-Eigenschaften stehen würde. 

For a complete list of properties and their order, please see the [property order for Stylelint](https://github.com/stormwarning/stylelint-config-recess-order) used by [Bootstrap](https://getbootstrap.com).
Ein komplette Liste von Eigenschaften und deren Reihenfolge ist in der [Eigenschaften Reihenfolge für Stylelint](https://github.com/stormwarning/stylelint-config-recess-order) zu finden, die von [Bootstrap](https://getbootstrap.com) genutzt wird.
</div>

```scss
.declaration-order {
  // Positionierung
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  // Box-Modell
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;

  // Typografie
  font: normal 14px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
  text-decoration: underline;

  // Visuell
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  // Sonstiges
  opacity: 1;
}
```

<div markdown="1">
### Logische Eigenschaften

Logische Eigenschaften sind Alternativen zu direktionalen und dimensionalen Eigenschaften, die auf abstrakten Begriffen wie *block* und *inline* basieren. Standardmäßig bezieht sich block auf die vertikale Richtung (oben und unten), während sich inline auf die horizontale Richtung (rechts und links) bezieht. Du kannst diese Werte in CSS in allen modernen Browsern verwenden.

**Warum logische Eigenschaften verwenden?** Nicht jede Sprache fließt von links nach rechts wie Englisch, also muss der ["writing mode" (Englisch)](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode) flexibel gehalten werden. Mit logischen Eigenschaften kannst du einfach Sprachen unterstützen, die auch horizontal oder vertiakl geschrieben werden können (wie Chinesisch, Japanisch und Koreanisch). Außerdem sind sie meist kürzer und einfacher zu schreiben.

**Weitere Informationen:**

- [CSS Logical Properties and Values – MDN (Englisch)](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties)
- [CSS Logical Properties and Values — CSS Tricks (Englisch)](https://css-tricks.com/css-logical-properties-and-values/)
- [CSS Writing Modes – MDN (Englisch)](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Writing_Modes)
</div>

```scss
// Ohne logische Eigenschaften
.element {
  margin-right: auto;
  margin-left: auto;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
}

// Mit logischen Eigenschaften
.element {
  margin-inline: auto;
  border-block: 1px solid #eee;
}
```

<div markdown="1">
### Farben

Mit der Unterstützung von [CSS Color Levels 4 (Englisch)](https://www.w3.org/TR/css-color-4/) [in allen wichtigen Browsern](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgb#space-separated_values), sind `rgba()` und `hsla()`  jetzt Aliase für `rgb()` und `hsl()`, was bedeutet, dass Alpha-Werte in `rgb()` und `hsl()` geändert werden können. Damit einher geht die Unterstützung der neuen, durch Leerzeichen getrennten Syntax für Farbwerte. Für die Kompatibilität mit zukünftigen CSS-Farbfunktionen sollte diese neue Syntax verwendet werden.

Unabhängig von Farbwerten und der Syntax, stelle immer sicher, dass deine Farbauswahl die [WCAG Mindestkontrastverhältnisse (Englisch)](https://webaim.org/articles/contrast/) erfüllen (4.5:1 für 16px und kleiner, 3:1 für größeres).

**Weitere Informationen:**

- [Smashing Magazine - A Guide To Modern CSS Colors (Englisch)](https://www.smashingmagazine.com/2021/11/guide-modern-css-colors/)
- [`rgb()` - MDN (Englisch)](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgb)
</div>

```css
.element {
  color: rgb(255 255 255 / .65);
  background-color: rgb(0 0 0 / .95);
}
```

<div markdown="1">
### Vermeide `@import`

Verglichen mit `<link>`s, ist `@import` langsamer, fordert eine zusätzliche Seite an und kann andere unvorhergesehene Probleme hervorrufen. Vermeide sie deshalb und verwende einen anderen Ansatz:

- Benutze mehrere `<link>` Elemente
- Kompiliere dein CSS mit einem Preprozessor wie [Sass](https://sass-lang.com/) oder [Less](https://lesscss.org/) in eine einzige Datei
- Verkette deine CSS Dateien mit Funktionen die in Rails, Jekyll oder anderen Umgebungen bereitgestellt werden

Für mehr Informationen, [ließ diesen Artikel von Steve Souders (Englisch)](https://www.stevesouders.com/blog/2009/04/09/dont-use-import/).

</div>

```html
<!-- Benutze link-Elemente -->
<link rel="stylesheet" href="core.css">

<!-- Vermeide @import -->
<style>
  @import url("more.css");
</style>
```

<div markdown="1">
### Media Query Platzierung

Platziere Media Queries so nah wie möglich an den zugehörigen Regelsätzen. Fasse sie nicht alle in einem separaten Stylesheet oder am Ende des Dokuments zusammen. Das macht es für die Leute nur leichter, sie in Zukunft zu übersehen. Hier findest du einen typischen Aufbau.

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
### Einzelne Deklarationen

In Fällen, in denen ein Regelsatz **nur eine Erklärung** enthält, sollten zur besseren Lesbarkeit und schnelleren Bearbeitung die Zeilenumbrüche entfernt werden. Jeder Regelsatz mit mehreren Deklarationen sollte in separate Zeilen aufgeteilt werden.

Der Schlüsselfaktor hier ist die Fehlererkennung, z.B. ein CSS-Validator, der einen Syntaxfehler in Zeile 183 meldet. Mit einer einzelnen Deklaration ist es unmöglich, den Fehler zu übersehen. Mit mehreren Deklarationen sind getrennte Zeilen allerdings ein Muss, zu deinem eigenen Wohl.

</div>

```scss
// Einzelne Deklarationen in einer Zeile
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

// Mehrere Deklarationen, eine pro Zeile
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
### Kurzschreibweisen

Beschränke die Verwendung von Deklarationen in Kurschreibweise auf Fälle, in denen alle verfügbaren Werte explizit festgelegt werden müssen. Zu den häufig überbenutzten Eigenschaften in Kurzschreibweise gehören:

- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

Normalerweise müssen nicht alle Werte, die eine Eigenschaft in Kurzschreibweise darstellt, gesetzt werden. HTML-Überschriften legen beispielsweise nur den oberen und unteren Rand fest, so dass bei Bedarf nur diese beiden Werte überschrieben werden. Ein `0`-Wert bedeutet, dass entweder ein Standardwert des Browsers oder ein zuvor festgelegter Wert außer Kraft gesetzt wird.

Die exzessive Nutzung von Eigenschaften in Kurzschreibweise führt zu schlampigeren Code mit unnötigen Überschreibungen und ungewollten Nebeneffekten. 

Das Mozilla Developer Network hat einen großartigen Artikel über [Eigenschaften in Kurzschreibweise](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) für alle, die mit der Notation und deren Verhalten nicht vertraut sind.

</div>

```scss
// Schlechtes Beispiel
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

// Gutes Beispiel
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

<div markdown="1">
### Verschachtelungen in Präprozessoren

Vermeide unnötige Verschachtelungen in Präprozessoren, wann immer dies möglich ist–halte es einfach und vermeide umgekehrte Verschachtelungen. Ziehe Verschachtelungen nur dann in Betracht, wenn sich Stile auf ein übergeordnetes Element beziehen müssen und wenn mehrere Elemente verschachtelt werden sollen.

**Weitere Informationen:**

- <a href="https://markdotto.com/2015/07/20/css-nesting/">Nesting in Sass and Less (Englisch)</a>
</div>

```scss
// Ohne Verschachtelung
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// Mit Verschachtelung
.table > thead > tr {
  > th { … }
  > td { … }
}
```

<div markdown="1">
### Operatoren in Präprozessoren

Schließe alle mathematischen Operationen in Klammern, mit einem Leerzeichen zwischen Werten, Variablen und Operatoren, ein, um die Lesbarkeit zu verbessern.

</div>

```scss
// Schlechtes Beispiel
.element {
  margin: 10px 0 @variable*2 10px;
}

// Gutes Beispiel
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```

<div markdown="1">
### Kommentare

Code wird von Menschen geschrieben und gepflegt. Stelle daher sicher, dass dein Code anschaulich, gut auskommentiert und für andere zugänglich ist. Gute Kommentare vermitteln den Kontext oder Sinn. Wiederhole nicht einfach nur den Namen einer Komponente oder Klasse. Verwende die `//`-Syntax, wenn du CSS mit Präprozessoren schreibst. Entferne alle Kommentare für die Production-State. 

Achte darauf, dass größere Anmkerungen in vollständigen Sätzen und allgemeine Notizen in kurzen Sätzen geschrieben werden.
</div>

```scss
// Schlechtes Beispiel
// Modal header
.modal-header {
  ...
}

// Gutes Beispiel
// Wrapping element für .modal-title und .modal-close
.modal-header {
  ...
}
```

<div markdown="1">
### Klassennamen

- Halte Klassen in Kleinbuchstaben und benutze Bindestriche (keine Unterstriche oder camelCase). Bindestriche dienen als Unterbrechungen in verwandten Klassen (z.B. `.btn` und `.btn-danger`).
- Vermeide übermäßige und willkürliche Kurzschreibweisen. `.btn` ist nützlich für _button_, aber `.s` bedeutet gar nichts.
- Halte Klassen so kurz und prägnant wie möglich.
- Verwende aussagekräftige Namen; verwende strukturelle oder zweckmäßige Namen anstelle von präsentativen.
- Präfixe Klassen auf Grundlage der nächstgelegenen parent oder base Klasse.
- Benutze `.js-*`-Klassen um das Verhalten (im Gegensatz zum Stil) zu kennzeichnen, aber benutze diese Klassen nicht in CSS, sondern nur in Javascript.

Es ist auch sinnvoll, viele dieser Regeln bei der Erstellung von benutzerdefinierten Eigenschaften und Präprozessorvariablennamen anzuwenden.
</div>

```scss
// Schlechtes Beispiel
.t { ... }
.red { ... }
.header { ... }

// Gutes Beispiel
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

<div markdown="1">
### Selektoren

- Benutze Klassen anstelle von generischen Element-Tags für expliziteres und zuverlässigeres Styling, dass von deinem Markup unabhängig ist.
– Vermeide das Benutzen von mehreren Attribut-Selektoren (z.B. `[class^="..."]`) bei öfter vorkommenden Komponenten. Die Browser Performance wird davon beeinflusst. 
- Halte Selektroen kurz und limitiere die Anzahl von Elementen in jedem Selektor auf drei. 
- Wende Klassen nur auf die nächstgelegene übergeordnete Klasse an, wenn dies notwenidg ist (z.B. wenn keine vorangestellten Klassen verwendet werden).

**Weitere Informationen:**

- [Scope CSS classes with prefixes (Englisch)](https://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
- [Stop the cascade (Englisch)](https://markdotto.com/2012/03/02/stop-the-cascade/)
</div>

```scss
// Schlechtes Beispiel
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

// Gutes Beispiel
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

<div markdown="1">
### Child und nachkommende Selektoren

Wenn notwendig, kann es nützlich sein, den [child combinator (`>`)](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator) zu verweden, um die Kaskade einiger Stile in Elementen wie `<table>`, die oft rekursiv verschachtelt sind, zu begrenzen. Verwende ihn, um Stile auf die unmittelbaren Child-Elemente eines Parents zu beschränken, um spätere unnötige Überschreibungen zu vermeiden.
</div>

```css
.custom-table > tbody > tr > td,
.custom-table > tbody > tr > th {
  /* ... */
}
```

<div markdown="1">
### Organisation

- Organisiere Abschnitte des Codes nach Komponeten.
- Entwickle eine konsistente Hierarchie für Kommentare. 
- Nutze konsistenten Leerraum zu deinem Vorteil, wenn du Codeabschnitte beim Durchsuchen größerer Dokumente voneinander trennen willst.
- Wenn du mehrere CSS Dateien verwendest, unterteile sie nach Komponenten anstelle von Seiten. Seiten können neu angeordnet und Komponenten verschoben werden.
</div>

```scss
//
// Überschrift des Komponentenabschnitts 
//

.element { ... }


//
// Überschrift des Komponentenabschnitts 
//
// Manchmal muss optionaler Kontext für eine Komponente bereitgestellt werden. Tue das hier, wenn es wichtig genug ist.
//

.element { ... }

// Kontextuelle Sub-Komponente oder Modifikator
.element-heading { ... }
```
