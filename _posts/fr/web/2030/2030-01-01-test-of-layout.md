---
title: 'Premier Test de mise en forme'
i18n-key: test-of-layout
tags:
    - Typographie
sitemap: false
robots:
    noindex: true
    nofollow: true
slug: test-typo
---

> Ceci est un article destiné à tester le respect de certaines règles microtypographiques par mon site.  
> Ne tenez pas compte du contenu ci-dessous.

<!-- more -->

# h1 Heading 8-)

## h2 Heading

### h3 Heading

#### h4 Heading

##### h5 Heading

###### h6 Heading

## Horizontal Rules

***

***

## Typographic replacements

Enable typographer option to see result.

(c) (C) (r) (R) (tm) (TM) (p) (P) +-

test.. test... test..... test?..... test!....

!!!!!! ???? ,, -- ---

"Smartypants, double quotes" and 'single quotes'

### Jekyll microtypo

**Thin spaces**

Hello ! 4 px, 5 % ?

**Median point (french)**

Il·Elle est intéressé·e.  
Ils·Elles sont intéressé·e·s.

**Numeral**

She's n°3.

**Ellipsis**

I'm good...

**Ordinals (french)**

Si je double le 2ème, je deviens 1er.

**Non-break spaces**

2001 : l'odysée de l'espace

**Currencies**

* 599$, donc 599 €.
* $599, so € 599

**Multiply**

Resolution: 1024x768.

## Emphasis

**This is bold text**

**This is bold text**

_This is italic text_

_This is italic text_

~~Strikethrough~~

## Blockquotes

> Blockquotes can also be nested...
>
> > ...by using additional greater-than signs right next to each other...
> >
> > > ...or with spaces between arrows.
>
> <cite>Author</cite>

## Lists

Unordered

* Create a list by starting a line with `+`, `-`, or `*`
* Sub-lists are made by indenting 2 spaces:
  * Marker character change forces new list start:
    * Ac tristique libero volutpat at
    - Facilisis in pretium nisl aliquet
    * Nulla volutpat aliquam velit
* Very easy!

Ordered

1.  Lorem ipsum dolor sit amet
2.  Consectetur adipiscing elit
3.  Integer molestie lorem at massa

4)  You can use sequential numbers...
5)  ...or keep all the numbers as `1.`

## Code

Inline `code`

Indented code

    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code

Block code "fences"

```
Sample text here...
```

Syntax highlighting

```js
var foo = function(bar) {
  return bar++;
};

console.log(foo(5));
```

## Tables

| Option | Description                                                               |
| ------ | ------------------------------------------------------------------------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default.    |
| ext    | extension to be used for dest files.                                      |

Right aligned columns

| Option |                                                               Description |
| -----: | ------------------------------------------------------------------------: |
|   data | path to data files to supply the data that will be passed into templates. |
| engine |    engine to be used for processing templates. Handlebars is the default. |
|    ext |                                      extension to be used for dest files. |

## Links

https://www.autolink.com

[link text](https://borisschapira.com)

[link with title](https://borisschapira.com "title text!")

### [Footnotes](https://github.com/markdown-it/markdown-it-footnote)

Footnote 1 link[^first].

Footnote 2 link[^second].

Duplicated footnote reference[^second].

[^first]: Footnote **can have markup**

  and multiple paragraphs.

[^second]: Footnote text.

### [Definition lists](https://github.com/markdown-it/markdown-it-deflist)

Term 1

: Definition 1
with lazy continuation.

Term 2 with _inline markup_

: Definition 2

        { some code, part of Definition 2 }

    Third paragraph of definition 2.

_Compact style:_

Term 1
~ Definition 1

Term 2
~ Definition 2a
~ Definition 2b

### Abbreviations

This is HTML abbreviation example.

It converts "HTML", but keep intact partial entries like "xxxHTMLyyy" and so on.

\*[HTML]: Hyper Text Markup Language

### Custom containers

{% include canonical.html.liquid
    locale=page.locale
    title=page.title
    canonical=page.canonical
%}

### Insertion

Lorem ipsum dolor sit amet, <ins datetime="2018-12-26">consectetur</ins> adipiscing elit. Addebat etiam se in legem Voconiam iuratum contra eam facere non audere, nisi aliter amicis videretur. Traditur, inquit, ab Epicuro ratio neglegendi doloris. Amicitiam autem adhibendam esse censent, quia sit ex eo genere, quae prosunt.

<ins class="bloc" datetime="2018-12-26">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Addebat etiam se in legem Voconiam iuratum contra eam facere non audere, nisi aliter amicis videretur. Traditur, inquit, ab Epicuro ratio neglegendi doloris. Amicitiam autem adhibendam esse censent, quia sit ex eo genere, quae prosunt.</ins>


## Rich figcaptions

{% capture img_alt %}Deux post-its, comparant l'Agile façon Cargo Cult et les vraies livraisons successives{% endcapture %}
{% capture img_caption %}"<a href="https://www.flickr.com/photos/psd/9588038559" title="Lien vers la photo sur Flickr">Doing Agile, being Agile</a>", par <a href="https://www.flickr.com/photos/psd/" title="Profil Flickr de Paul Downey">Paul Downey</a> — <a href="https://creativecommons.org/licenses/by/2.0/" class="photo-license-url" rel="license cc:license" target="_newtab" ><span>Certains droits réservés</span></a>{% endcapture %}
{% include rwd-image.html.liquid
path="/assets/images/2017-04-02/doing_vs_being_agile.jpg"
alt=img_alt
caption=img_caption
%}
