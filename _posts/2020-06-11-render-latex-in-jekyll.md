---
layout: post
title: Rendering LaTeX in Jekyll pages
date: 2020-06-11 08:24
# description: 
img: R0000558.jpg
fig-caption: Barkway barley
fig-attrib: Nick Hood
published: yes
katex: yes
tags:
- Jekyll
- LaTeX

# permalink:
---
I wanted to render a formula for standard deviation on a page in a site built on Jekyll. Sal Khan's [Khan Academy](https://www.khanacademy.org/) has tackled a similar problem and developed their own solution. Not only have they done that, but they have made it available to the world under an MIT Licence. That solution is [KaTeX](https://katex.org/).

## $$\KaTeX$$
Described as "The fastest math typesetting library for the web", it has no dependencies and renders very quickly on all major browsers. The API is simple and openly accessible, with javascript libraries publicly hosted in a CDN. It is also implemented in [kramdown](https://kramdown.gettalong.org/), the MIT-licensed markdown parser, which makes it an ideal solution for sites that are built on Jekyll, such as those hosted on github pages.

To implement it in a Jekyll site, the markdown parser should be set in config.yml:

```yaml
markdown: kramdown
```
In the `<head>` section, perhaps in the included file `_includes/head.html`, add the KaTeX libraries and css:

```html
  <!-- KaTeX -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">

  <!-- The loading of KaTeX is deferred to speed up page rendering -->
  <script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>

  <!-- To automatically render math in text elements, include the auto-render extension: -->
  <script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous"
      onload="renderMathInElement(document.body);"></script>
```

 In my implementation, I set a flag in the yaml header of any page that requires \\(\LaTeX\\), for example:

```yaml
---
layout: post
title: Render LaTeX in Jekyll pages
date: 2020-06-11 08:24
published: yes
katex: yes
tags:
- Jekyll
- LaTeX
---
```

Then conditionally output the header code above only in pages that need to load the css and script:

```liquid
{% raw %}
{% if page.katex %}
  <!-- KaTeX -->
  .
  . etc.
  .
{% endif %}
{% endraw %}
```
## Using it
Having set the `katex` flag, I can now type LaTeX code either as display (slightly larger and in its own block on the page), or inline:

```tex
$$\LaTeX code$$     % (for inline)
\\(\LaTeX code\\)   % (also for inline)
\\[\LaTeX code\\]   % (for display)
```
The $$\KaTeX$$ script converts the `$$` code above into either `\\(` inline or `\\[` display syntax
which is output as html:

```html
<p>\(\LaTeX code\)     % (inline)</p>
<p>\[\LaTeX code\]     % (display)</p>
```
and renders thus:

\\(\LaTeX code\\)
\\[\LaTeX code\\]

## Example: binomial coefficient
In the markdown for this page, if I type:

```
\\[
    \binom{n}{k} = \frac{n!}{k!(n-k)!}
\\]
```

Jekyll and kramdown will output this html:

```html
<p>
\[
    \binom{n}{k} = \frac{n!}{k!(n-k)!}
\]</p>
```

In the client browser, the KaTeX javascript will render thus:
\\[
    \binom{n}{k} = \frac{n!}{k!(n-k)!}
\\]


## Caveats
Notice this solution does not render $$\LaTeX$$ from the server side. All of the rendering is done on the client using the javascript loaded in the `head` of the page. It just does it very, very quickly.
