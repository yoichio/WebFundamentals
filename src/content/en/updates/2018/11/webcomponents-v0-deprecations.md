project_path: /web/_project.yaml
book_path: /web/updates/_book.yaml
description: Web Components v0 deprecation and removal in Chrome73 to help you plan.

{# wf_updated_on: 2018-11-29 #}
{# wf_published_on: 2018-12-03 #}
{# wf_tags: deprecations,removals,chrome73,webcomponents,origintrials #}
{# wf_blink_components: Blink>DOM #}
{# wf_featured_image: /web/updates/images/generic/warning.png #}
{# wf_featured_snippet: Web Components v0 deprecation and removal in Chrome 73 to help you plan.#}

# Web Components v0 deprecation {: .page-title }

{% include "web/_shared/contributors/yoichiosato.html" %}

A part of web interoperability for [Web Components v1](/web/updates/2017/01/webcomponents-org),
Chrome is removing
[Shadow DOM v0](https://www.html5rocks.com/en/tutorials/webcomponents/shadowdom/),
[Custom Elements v0](https://www.html5rocks.com/en/tutorials/webcomponents/customelements/)
 and [HTML Imports](https://www.html5rocks.com/en/tutorials/webcomponents/imports/)
  in Mar, 2019 at Chrome 73.

[Intent to Deprecate](https://groups.google.com/a/chromium.org/forum/#!msg/blink-dev/h-JwMiPUnuU/sl79aLoLBQAJ)


## Motivation

Shadow DOM v0, Custom Elements v0, and HTML Imports (hereinafter, called v0 features)
 were launched in 2014, but
they did not get adopted by other browser engines. Instead, Shadow DOM v1,
Custom Elements v1, and ES modules are widely adopted by various browser engines
today. Chrome has shipped Shadow DOM v1 / Custom Elements v1 in 2016 and ES
modules in 2017.

- Shadow DOM v0: [Chromestatus Tracker](https://www.chromestatus.com/feature/4507242028072960) &#124;
 [Chromium Bug](https://crbug.com/671907)
- Custom Elements v0: [Chromestatus Tracker](https://www.chromestatus.com/feature/4642138092470272)  &#124;
 [Chromium Bug](https://crbug.com/660759)
- HTML Imports: [Chromestatus Tracker](https://www.chromestatus.com/feature/4507242028072960)  &#124;
[Chromium Bug](https://crbug.com/766694)

### Why removing them at once?

Chrome usually removes features one by one, but why at once for these features this time?  
Since launched, we found that they are often used together.
Especially [webcomponentsjs polyfill](https://github.com/WebComponents/webcomponentsjs)
 was originally designed to simulate the v0 features on other
browsers and not do so on Chrome being removed each feature randomly.  
For safer/lesser troublesome migration off from the features, we've desided to
remove them at one.

## Migration support
If your site and/or libirary is using this features, you should upgrade them.  
Use `$ chrome --disable-blink-features=ShadowDOMV0,CustomElementsV0,HTMLImports` 
on command line to launch Chrome disabled v0 features for testing if your site works without those APIs.

### Polyfill

Now webcomponents polyfill supports v0 features on the all-v0-disabled Chrome. A web site using the polyfill should continue to work.  
This is also another option for the web authors.
You can install the polyfill on the site using v0 features directly to keep
it working.  
There are also other alternative polyfills for each feature (e.g.
[AshleyScirra’s HTML Imports polyfill](https://github.com/AshleyScirra/html-imports-polyfill)).


### Reverse Origin Trial

For web authors that don't much time to Mar, 2019 at Chrome 73,
we're preparing called Reverse [Origin Trial](https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/developer-guide.md)
 where you can use each removed feature with tokens after Chrome 73 for one year
 to Chrome 81.
Sign up form is coming. Stay tuned.


## Remove Shadow DOM v0
Shadow DOM v0 API `Element.createShadowRoot()` is removed.  
Instead Chrome has v1 API `Element.attachShadow()` to create Shadow Root.
V1 is not backward compatible to v0 in many points (distribution, styling, focusing,,,).
See a [document](https://hayato.io/2016/shadowdomv1/) for further comparing and
our [document](/web/fundamentals/web-components/shadowdom) describes v1 functions and usage.


## Remove Custom Elements v0
Custom Elements v0 API `document.registerElement()` is removed.  
Instead Chrome has v1 API `window.customElements.define()` to define Custom Element.  
V1 is not backward compatible to v0.  
Our [document](/web/fundamentals/web-components/customelements) describes v1 functions and usage.


## Remove HTML Imports

HTML Imports is removed.  
[HTML Modules](https://github.com/w3c/webcomponents/issues/645) will serve
similar functionality.  
Though Chrome doesn't have any direct replacement for HTML Imports yet, Chrome is removing this for healthy web:
a site HTML Imports mandatory doesn't work on other browsers.

{% include "web/updates/_shared/deprecations-policy.html" %}

{% include "web/_shared/rss-widget-updates.html" %}

{% include "comment-widget.html" %}
