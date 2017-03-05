# Lazy Import
[![Build status][travis-badge]][travis-url] [![Bower dependencies][bowerdeps-badge]][bowerdeps-url] ![Version][bower-badge] ![Size][size-badge] [![Published][webcomponents-badge]][webcomponents-url]

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
Set the path to your element import in the `href` property, then set `active` when you want to import it

```html
<lazy-import href="path/to/my-element.html">
  <my-element></my-element>
</lazy-import>

<!-- Import and show <my-element> -->
<script>
  document.querySelector('lazy-import').active = true;
</script>
```

`lazy-import` only imports a component once (the first time `active` is `true`, or if a new `href` is set), regardless of how many times `active` changes. When `active` is false, `lazy-import` is set to `display: none`, so your component is not in the document flow until it is imported.

### Lazifying SPA routers
Use `lazy-import` with simple content switchers like Polymer's [`iron-pages`][iron-pages] to turn them into performant, lazy-loading component routers.

Make your router set the `active` prop on the active route, and wrap view components in `lazy-import`. That way both the import and your element will be hidden when inactive, and routing will automatically import the view component lazily

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
`loading`    | `Boolean` | True while an import is being fetched & parsed


--

MIT © Sean King <sean@seanking.org>

[webcomponents]: https://github.com/webcomponents/webcomponentsjs

[bower-badge]: https://img.shields.io/bower/v/lazy-import.svg
[bowerlicense-badge]: https://img.shields.io/bower/l/lazy-import.svg
[travis-badge]: https://img.shields.io/travis/seaneking/lazy-import.svg
[travis-url]: https://travis-ci.org/seaneking/lazy-import
[bowerdeps-badge]: https://img.shields.io/gemnasium/seaneking/lazy-import.svg
[bowerdeps-url]: https://gemnasium.com/bower/lazy-import
[size-badge]: https://badges.herokuapp.com/size/github/seaneking/lazy-import/master/lazy-import.html?gzip=true&color=blue
[webcomponents-badge]: https://img.shields.io/badge/webcomponents.org-published-blue.svg
[webcomponents-url]: https://www.webcomponents.org/element/seaneking/lazy-import.sv
[iron-pages]: https://www.webcomponents.org/element/PolymerElements/iron-pages
