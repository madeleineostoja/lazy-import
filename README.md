# Lazy Import
[![Build status][travis-badge]][travis-url] [![Bower dependencies][bowerdeps-badge]][bowerdeps-url] ![Version][bower-badge] [![Published][webcomponents-badge]][webcomponents-url]

Declaratively import a HTML component when you're ready to use it. Useful for improving the performance of routing in SPAs built on Web Components.

### Installation

Install lazy-import with Bower (Yarn support coming soon)

```sh
$ bower i lazy-import --save
```

Import it into the `<head>` of your document

```html
<link rel="import" href="/bower_components/lazy-import/lazy-import.html">
```

#### Polyfills for cross-browser support

lazy-import relies on emerging standards, for full cross-browser support include the [Web Components Lite][webcomponents] polyfill.

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/webcomponentsjs/0.7.24/webcomponents-lite.min.js"></script>
```


### Basic usage
Wrap your element in `lazy-import`, and set `active` when you're ready to use it

```html
<lazy-import href="path/to/my-element.html">
  <my-element></my-element>
</lazy-import>

<!-- Import and show <my-element> -->
<script>
  document.querySelector('lazy-import').active = true;
</script>
```

Toggling the `active` property also shows/hides the `lazy-import` element, so you element isn't in the document flow until it is imported.

`lazy-import` only imports a component once (the first time `active` is `true`, or if a new `href` is set).

### Lazifying SPA routers
Use `lazy-import` with simple content switchers like Polymer's [`iron-pages`][iron-pages] to turn them into performant, lazy-loading component routers.

Make your router set the `active` prop on the active route, and wrap view components in `lazy-import`

```html
<iron-pages
  attr-for-selected="data-route"
  selected-attribute="active"
>
  <lazy-import data-route="app" href="/path/to/my-app">
    <my-app></my-app>
  </lazy-import>

  <lazy-import data-route="other-view" href="/path/to/other-view">
   <other-view></other-view>
  </lazy-import>
</iron-pages>
```

### Properties

Property     | Type      | Description                                                  
------------ | --------- | ---------------
`href`       | `String`  | Path to import when active                                   
`active`     | `Boolean` | Whether to import component and show `lazy-import`           
`activeAttr` | `String`  | Optional attribute to set on children when active            
`onLoad`     | `String`  | Optional callback to execute when import successfully loaded 


--

MIT © Sean King <sean@seanking.org>

[webcomponents]: https://github.com/webcomponents/webcomponentsjs

[bower-badge]: https://img.shields.io/bower/v/lazy-import.svg
[bowerlicense-badge]: https://img.shields.io/bower/l/lazy-import.svg
[travis-badge]: https://img.shields.io/travis/seaneking/lazy-import.svg
[travis-url]: https://travis-ci.org/seaneking/lazy-import
[bowerdeps-badge]: https://img.shields.io/gemnasium/seaneking/lazy-import.svg
[bowerdeps-url]: https://gemnasium.com/bower/lazy-import
[webcomponents-badge]: https://img.shields.io/badge/webcomponents.org-published-blue.svg
[webcomponents-url]: https://www.webcomponents.org/element/seaneking/lazy-import.svg
[iron-pages]: https://www.webcomponents.org/element/PolymerElements/iron-pages
