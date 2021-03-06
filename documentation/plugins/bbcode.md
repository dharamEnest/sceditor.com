---
layout: doc
title: BBCode - Plugin
permalink: /documentation/plugins/bbcode/
categories:
    - Docs
---

## BBCode Plugin <a id="bbcode"></a>

This plugin will convert the output of SCEditor into BBCode. To add custom BBCodes see the [Custom BBCodes page](/documentation/custom-bbcodes/).


### Initialise <a id="initialise"></a>

To enable the BBCode plugin just add `bbcode` to the `plugins` option. e.g.

<pre class="prettyprint linenums">
&lt;script&gt;
$(function() {
	$("textarea").sceditor({
		plugins: "bbcode",
		style: "minified/jquery.sceditor.default.min.css"
	});
});
&lt;/script&gt;
</pre>


### Custom BBCodes <a id="custom-bbcodes"></a>

To create custom BBCodes see the [Custom BBCodes page](/documentation/custom-bbcodes/).


### Parser Options <a id="parser-options"></a>

To set parser options, use the [parserOptions option](/documentation/options/#parserOptions) when creating the editor.

e.g.

<pre class="prettyprint linenums">
&lt;script&gt;
$(function() {
	$("textarea").sceditor({
		plugins: "bbcode",
		style: "minified/jquery.sceditor.default.min.css",

		parserOptions: {
			breakBeforeBlock: false,
			breakStartBlock: false
			// ect.
		}
	});
});
&lt;/script&gt;
</pre>


### breakBeforeBlock

**breakBeforeBlock** *Boolean* Defaults to `false`

If to add a new line before block level elements

This can be overridden by individual BBCodes using the `breakBefore` property.


### breakStartBlock

**breakStartBlock** *Boolean* Defaults to `false`

If to add a new line after the start of block level elements

This can be overridden by individual BBCodes using the `breakStart` property.


### breakEndBlock

**breakEndBlock** *Boolean* Defaults to `false`

If to add a new line before the end of block level elements

This can be overridden by individual BBCodes using the `breakEnd` property.


### breakAfterBlock

**breakAfterBlock** *Boolean* Defaults to `true`

If to add a new line after block level elements.

This can be overridden by individual BBCodes using the `breakAfter` property.


### removeEmptyTags

**removeEmptyTags** *Boolean* Defaults to `true`

If to remove empty tags.

This can be overridden by individual BBCodes using the `allowsEmpty` property.


### fixInvalidNesting

**fixInvalidNesting** *Boolean* Defaults to `true`

If to fix invalid nesting, like block level elements inside inline elements.

For example.

<pre class="prettyprint linenums lang-bbcode">
[inline]testing[block]test[/block]123[/inline]
</pre>

Would become:

<pre class="prettyprint linenums lang-bbcode">
[inline]testing[/inline][block]test[/block][inline]123[/inline]
</pre>


### fixInvalidChildren

**fixInvalidChildren** *Boolean* Defaults to `true`

If to fix invalid children. i.e. A tag which is inside a parent that doesn't allow that type of tag as a child.


### quoteType

**quoteType** *$.sceditor.BBCodeParser.QuoteType* Defaults to `$.sceditor.BBCodeParser.QuoteType.auto`

The default attribute quote type.

Should be one of the following values:

* **$.sceditor.BBCodeParser.QuoteType.always**  
  Always quote the attribute value
* **$.sceditor.BBCodeParser.QuoteType.never**  
  Never quote the attributes value
* **$.sceditor.BBCodeParser.QuoteType.auto**  
  Only quote the attributes value when it contains spaces ot equals




### Added methods <a id="methods"></a>

When the BBCode plugin is enabled, it will add the methods `toBBCode()` and `fromBBCode()` to the editor instance.

<article class="api method" markdown="1">
### <a id="toBBCode" href="#toBBCode">toBBCode()</a> <span class="since">Since: 1.4.3</span>

Converts HTML or a DOM node to a BBCode string.

In order for this method to convert YouTube embed codes into the `[youtube]`
tag, a `data-youtube-id` attribtue must be added to the YT embed code with the
value of the YouTube video it embeds.


#### Syntax

	var bbcode = instance.toBBCode(html);


#### Parameters

<div class="parameters">
<div class="parameter" markdown="1">
**html**  
Type: *[String](/api/types/#string)* or *[Node](/api/types/#node)*

The HTML string or DOM node to convert.
</div>
</div>


#### Return

Type: **[String](/api/types/#string)**
</article>


<article class="api method" markdown="1">
### <a id="fromBBCode" href="#fromBBCode">fromBBCode()</a> <span class="since">Since: 1.4.3</span>

Converts a string of BBCode into a string of HTML.


#### Syntax

	var html = instance.fromBBCode(bbcode[, asFragment]);


#### Parameters

<div class="parameters">
<div class="parameter" markdown="1">
**bbcode**  
Type: *[String](/api/types/#string)* or *[Node](/api/types/#node)*

The BBCode string to convert.
</div>
<div class="parameter" markdown="1">
**asFragment**  
Type: *[Boolean](/api/types/#bool)*
Default: `false`

If to convert the BBCode to a HTML fragment or if to wrap it in `div` tags. For example:

[b]Bold![/b] will convert to &lt;div&gt;&lt;strong&gt;Bold!&lt;/strong&gt;&lt;/div&gt;

but if `asFragment` is `true`, it will convert to:

[b]Bold![/b] will convert to &lt;strong&gt;Bold!&lt;/strong&gt;
</div>
</div>


#### Return

Type: **[String](/api/types/#string)**
</article>


#### Examples

<pre class="prettyprint linenums">
&lt;script&gt;
$(function() {
	$("textarea").sceditor({
		plugins: "bbcode",
		style: "minified/jquery.sceditor.default.min.css"
	});

	// Will be [b]Bold![/b]
	var bbcode       = $("textarea").sceditor('instance').toBBCode('&lt;strong&gt;Bold!&lt;/strong&gt;');

	// Will be &lt;div&gt;&lt;strong&gt;Bold!&lt;/strong&gt;&lt;/div&gt;
	var html         = $("textarea").sceditor('instance').fromBBCode('[b]Bold![b]');

	// Will be &lt;strong&gt;Bold!&lt;/strong&gt;
	var htmlFragment = $("textarea").sceditor('instance').fromBBCode('[b]Bold![b]', true);
});
&lt;/script&gt;
</pre>
