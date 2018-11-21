project_path: /web/_project.yaml
book_path: /web/updates/_book.yaml
description: A round up of the deprecations and removals in Chrome 71 to help you plan.

{# wf_updated_on: 2018-11-21 #}
{# wf_published_on: 2018-11-13 #}
{# wf_tags: deprecations,removals,chrome73,webcomponents,origintrials #}
{# wf_blink_components: Blink>DOM #}
{# wf_featured_image: /web/updates/images/generic/warning.png #}
{# wf_featured_snippet: Web Components v0 deprecation and removal in Chrome 73 to help you plan.#}

{% include "web/updates/_shared/see-all-dep-rem.html" %}

# Web Components v0 deprecation {: .page-title }

{% include "web/_shared/contributors/yoichiosato.html" %}

A part of web interoperability for [Web Components v1](/web/updates/2017/01/webcomponents-org),
we're deprecating Shadow DOM v0, Custom Element v0 and HTML Imports in Chrome 73.

[Intent to Deprecate](https://groups.google.com/a/chromium.org/forum/#!msg/blink-dev/h-JwMiPUnuU/sl79aLoLBQAJ)


## Motivation

Shadow DOM v0, Custom Elements v0, and HTML Imports were launched in 2014, but
they did not get adopted by other browser engines. Instead, Shadow DOM v1,
Custom Elements v1, and ES modules are widely adopted by various browser engines
today. Chrome has shipped Shadow DOM V1 / Custom Elements V1 in 2016 and ES
modules in 2017.

- Shadow DOM v0: [Chromestatus Tracker](https://www.chromestatus.com/feature/4507242028072960) &#124;
 [Chromium Bug](https://crbug.com/671907)
- Custom Elements v0: [Chromestatus Tracker](https://www.chromestatus.com/feature/4642138092470272)  &#124;
 [Chromium Bug](https://crbug.com/660759)
- HTML Imports: [Chromestatus Tracker](https://www.chromestatus.com/feature/4507242028072960)  &#124;
[Chromium Bug](https://crbug.com/766694)

### Why at once?

Since then, we also found that in many real-world use cases, Shadow DOM V0,
Custom Elements V0, HTML Imports were used together, and instead of getting each
 of them migrated respectively, getting all of them migrated to today’s standards
 at once, or at least use the polyfill would make it less troublesome, easier to
 migrate, rather than fighting with every edge case of combination of polyfill
  and native implementation.

## Migration support
If you are using this features, please consider migrating to the new API or
upgrading your Polymer library.
Use `--disable-blink-features=ShadowDOMV0,CustomElementsV0,HTMLImports` for
 testing if your site works without those APIs.

## Remove Shadow DOM v0
`Element.createShadowRoot()` will be removed. Instead we have `Element.attachShadow()`
to create Shadow Root.
If your existing components don't use distribution, replacing with
`Element.attachShadow({mode:"open"})` might work.
Otherwise, Shadow DOM v1 is not backward compatible to v0.
See a [document](https://hayato.io/2016/shadowdomv1/) for further comparing and
our [document](/web/fundamentals/web-components/shadowdom) describes v1 functions and usage.


## Remove Custom Elements v0
`document.registerElement()` will be replaced by  `window.customElements.define()`.
If you are calling `document.registerElement('my-button', MyButton)` with class name rather than prototype,
`window.customElements.define('my-button', MyButton)` should work.
Our [document](/web/fundamentals/web-components/customelements) describes v1 functions and usage.


## Remove HTML Imports

HTML Imports will be removed. Similar functionarity will be served as HTML Modules.
Though HTML Module is still under [spec discussion](https://github.com/w3c/webcomponents/issues/645)
and we don't have any direct replacement for HTML Imports yet, we're deprecating this for healthy web:
a site HTML Imports mandatory doesn't work on other browsers.
If you're using HTML Imports, polyfill emulates it on `--disable-blink-features=HTMLImports` Chrome.


## Reverse Origin Trial

For web authors that don't much time to M73,
we're preparing called Reverse [Origin Trial](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md)
 where you can use the deprecated features with tokens after M73 for one year
 to M81.
Sign up form is coming. Stay tuned.

## Polymer/Polyfill
It depends on which version you're using:

- A web site using polyfills should continue to work.
- If you're using Polymer 1.x or 2.x, you'll need to make sure you're loading the polyfills.
- If you're using Polymer 3.x or LitElement, the deprecation should not affect you.

[Polymer teams' document](https://www.polymer-project.org/blog/2018-10-02-webcomponents-v0-deprecations)
well introduces more detail gudelines.

{% include "web/updates/_shared/deprecations-policy.html" %}

{% include "web/_shared/rss-widget-updates.html" %}

{% include "comment-widget.html" %}
