# react-laybox [![NPM package version](https://img.shields.io/npm/v/react-laybox.svg?style=flat-square)](https://www.npmjs.com/package/react-laybox) [![Dependency Status](https://david-dm.org/monkeydri/react-laybox.svg?style=flat-square)](https://david-dm.org/monkeydri/react-laybox) [![devDependencies Status](https://david-dm.org/monkeydri/react-laybox/dev-status.svg?style=flat-square)](https://david-dm.org/monkeydri/react-laybox?type=dev) [![NPM downloads](https://img.shields.io/npm/dm/react-laybox.svg?style=flat-square)](https://www.npmjs.com/package/react-laybox) [![HitCount](http://hits.dwyl.io/monkeydri/react-laybox.svg)](http://hits.dwyl.io/monkeydri/react-laybox) [![Build Status](https://img.shields.io/travis/monkeydri/react-laybox.svg?style=flat-square)](https://travis-ci.org/monkeydri/react-laybox) [![codecov.io](https://img.shields.io/codecov/c/github/monkeydri/react-laybox/master.svg?style=flat-square)](http://codecov.io/github/monkeydri/react-laybox?branch=master) [![Inline docs](http://inch-ci.org/github/monkeydri/react-laybox.svg?style=flat-square&branch=master)](http://inch-ci.org/github/monkeydri/react-laybox) [![JavaScript Style Guide: Good Parts](https://img.shields.io/badge/code%20style-goodparts-brightgreen.svg?style=flat-square)](https://github.com/dwyl/goodparts "JavaScript The Good Parts")

Set of react components to build any layout with ease, combine CSS Flexbox, CSS Grid and other CSS tricks.

# Install

`npm install react-laybox`

# Demo

codepen // TODO

# Usage

```js
import { Row, Column } from 'react-laybox';
```

```jsx
<div style={{ width: '100%', height: '100%' }}>
	<Row x="center" y="center" style={{ height: '30%' }} debug>
		<p>#1<p/>
		<p>#2<p/>
		<p>#3<p/>
	<Row />
</div>
```

```jsx
<div style={{ width: '100%', height: '100%' }}>
	<Row x="left" y="bottom" style={{ height: '30%' }} debug>
		<p>#1<p/>
		<p>#2<p/>
		<p>#3<p/>
	<Row />
</div>
```

```jsx
<div style={{ width: '100%', height: '100%' }}>
	<Column x="center" y="center" style={{ width: '20%' }} debug>
		<p>#1<p/>
		<p>#2<p/>
		<p>#3<p/>
	<Column />
</div>
```

# Why

## problem

Despite all the awesome tools available for styling ([SASS](https://sass-lang.com/), [CSS Modules](https://github.com/css-modules/css-modules), [Autoprefixer](https://github.com/postcss/autoprefixer), [CSS Loader](https://github.com/webpack-contrib/css-loader)...) design HTML UI is fun, however laying out those UI elements is still cumbersome.

To write simple UI nowadays, which fits every screen size, you have few solutions, but to me they each have their drawbacks :

- [CSS Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) => layout based on content, makes it hard to get a layout defined by container (where inner content shrink/expand).
- [CSS Grid](https://www.w3schools.com/css/css_grid.asp) => layout based on grid, makes it hard to adapt layout when content gets bigger.
- Grid layout framework (such as the one provided by [Bootstrap](https://github.com/twbs/bootstrap)) => forces you to think in terms of Columns inside Rows, arbitrary breakpoints responsive and most importantly predefined layout which does not adapt to inner content.

Each of those solution work great but only for specific use cases, and does not prevent problems once you start adding real things inside your layout, for example a React Component which do not use same CSS display than your layout => overflows, unresponsive.
As a result you will still need to get your hands dirty deep down in the CSS, and wiggle with things such as `min-height: 0` or other CSS tricks until *things look good*. This is not fun and this is a huge waste of time.

## simple API

If, like me, you are tired of this and just want to "always keep this div at the center" + "keep footer at the bottom unless there is too much vertical content" or "put those divs side by side and keep them 50% of width or height no matter how much content is inside", then you will love [react-laybox](https://github.com/monkeydri/react-laybox).

The goal of this project is to provide React components, used as containers, with an intuitive API to layout content quickly.

## code readibility

The second goal of this project is to make easier to understand layout from your code. Splitting CSS from your HTML does not help, and CSS media-queries make it even harder to follow.

React is the perfect match for [laybox](https://github.com/monkeydri/laybox) as using `<Component />`s instead of `<div>`s with multiple classes makes your code clearer because it is easier to understand :
- where your blocks stops, since each Component has a different name (see exemples TODO).
- how content is layed out, since the Component name reflects its purpose (`<Row />`, `<Column />`).

# Props

## props that applies to self (container)

| Name | Type | Description | Default Value |
| -------------  | ---- | ----------- | ------- |
| grow  | number or bool | flex-grow. grow={false} => 0, grow={true} -> 1. | 0 |

## props that applies to items (children)

| Name | Type | Description | Default Value |
| -------------  | ---- | ----------- | ------- |
| x  | enum 'left', 'center', 'right', 'space', 'stretch' | horizontal aligment of items inside element | 'center' |
| y | enum 'top', 'center', 'bottom', 'space', 'stretch' | vertical aligment of items inside element | 'center' |

## custom styling props

| Name | Type | Description | Default Value |
| -------------  | ---- | ----------- | ------- |
| className | string | pass custom class to resulting div | '' |
| style | object | pass custom style to resulting div | {} |

## debug props

| Name | Type | Description | Default Value |
| -------------  | ---- | ----------- | ------- |
| debug | bool | add border and color to div | false |

# Notes

## About `<Rows />` & `<Columns />`

API to align inner components differs from [CSS Flexbox](https://www.w3schools.com/css/css3_flexbox.asp), it is based on left/right/top/bottom rather than flex-start/flex-end. It allows to get get same reference system wether using a `<Column />` or a `<Row />` layout.

Unlike other UI frameworks which provides Grid layout like Bootstrap, Foundation or Semantic-UI you don't need to put `<Column />`s in row. A `<Column />` is a container which stacks its children one below the other, as such there is no reason nor need to put it inside a `<Row />` and this prevents adding dummy component in your code and resulting `<div>`s in the DOM tree.

## Other considerations

react-laybox overcomes some of the [CSS Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) limitations such as the impossibility to set max-height of a grown item in row mode (or max-width in column mode). // TODO

react-laybox allows to build full scaled layout ie. content will be resized based on container width. // TODO

# Dependencies

- React
- Prop Types

# Contributing [![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat-square)](https://github.com/monkeydri/react-laybox/issues)

# Licence

[MIT](LICENSE)