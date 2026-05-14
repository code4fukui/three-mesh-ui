# three-mesh-ui

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

<p align="center">
  <a href="https://www.npmjs.com/package/three-mesh-ui">
    <img alt="NPM" src="https://img.shields.io/npm/v/three-mesh-ui.svg"/>
  </a>
  <a href="https://github.com/felixmariotto/three-mesh-ui/blob/master/LICENSE">
    <img alt="MIT License" src="https://img.shields.io/github/license/felixmariotto/three-mesh-ui"/>
  </a>
</p>

<p align="center">
  <a href="https://felixmariotto.github.io/three-mesh-ui/"><strong>Live Examples</strong></a>
  &nbsp;|&nbsp;
  <a href="https://www.npmjs.com/package/three-mesh-ui"><strong>NPM</strong></a>
  &nbsp;|&nbsp;
  <a href="https://github.com/felixmariotto/three-mesh-ui/wiki"><strong>Documentation</strong></a>
  &nbsp;|&nbsp;
  <a href="https://github.com/felixmariotto/three-mesh-ui/wiki/Roadmap-&-Contributions"><strong>Contributing</strong></a>
</p>

📢 **v7.x.x is in evaluation!** Check out the latest developments here: https://github.com/felixmariotto/three-mesh-ui/pull/223

<a href="https://three-mesh-ui.herokuapp.com/#interactive_button">
  <img alt="Interactive buttons with hover and select states" target="_blank" src="https://felixmariotto.s3.eu-west-3.amazonaws.com/three-mesh-ui-teasers/buttons_opti.gif" width="45%">
</a>
<a href="https://three-mesh-ui.herokuapp.com/#hidden_overflow">
  <img alt="A text panel with scrolling and hidden overflow" target="_blank" src="https://felixmariotto.s3.eu-west-3.amazonaws.com/three-mesh-ui-teasers/hidden_overflow_opti.gif" width="45%">
</a>
<a href="https://three-mesh-ui.herokuapp.com/#nested_blocks">
  <img alt="A complex layout with nested containers and text alignment" target="_blank" src="https://felixmariotto.s3.eu-west-3.amazonaws.com/three-mesh-ui-teasers/nested_layout_opti.gif" width="45%">
</a>
<a href="https://three-mesh-ui.herokuapp.com/#keyboard">
  <img alt="An interactive 3D keyboard for text input" target="_blank" src="https://felixmariotto.s3.eu-west-3.amazonaws.com/three-mesh-ui-teasers/keyboard_opti.gif" width="45%">
</a>

## What is it?

**three-mesh-ui** is a library for building user interfaces in VR/AR experiences. It is built on top of and for [three.js](https://threejs.org).

Since it's impossible to use HTML/CSS to create user interfaces in a WebXR immersive session, this library was created to solve that problem. It provides a way to create 3D UIs that are themselves `THREE.Object3D` instances, ready to be added to any `THREE.Scene`.

It is not a framework, but a minimalist library with no dependency other than three.js.

## Features

- **VR/AR Ready**: Builds UIs as `THREE.Object3D` instances, perfect for immersive environments.
- **Declarative Layout**: Uses a Flexbox-like system with properties like `contentDirection`, `justifyContent`, and `alignItems` for easy and powerful layouts.
- **Text and Font Support**: Renders crisp text using MSDF (Multi-channel Signed Distance Field) fonts. Supports word-wrapping, letter-spacing, and overflow control.
- **Interactive Components**: Includes core components like `Block`, `Text`, and an interactive `Keyboard`.
- **Styling**: Customize components with rounded corners, borders, and backgrounds with opacity control.

## Quick Start

### Try it now

- **JSFiddle**: [Give it a try in this JSFiddle](https://jsfiddle.net/felixmariotto/y81rf5t2/44/)
- **react-three-fiber**: [Here is a CodeSandbox to get started](https://codesandbox.io/s/react-three-mesh-ui-forked-v7n0b?file=/src/index.js)

### Installation

```bash
npm install three-mesh-ui
```

⚠️ `three` is a peer dependency.

### Basic Usage

```javascript
import * as THREE from 'three';
import ThreeMeshUI from 'three-mesh-ui';

// In your scene creation
const container = new ThreeMeshUI.Block({
  width: 1.2,
  height: 0.7,
  padding: 0.05,
  justifyContent: 'center',
  alignItems: 'center',
  fontFamily: './assets/Roboto-msdf.json',
  fontTexture: './assets/Roboto-msdf.png',
});

const text = new ThreeMeshUI.Text({
  content: "Some text to be displayed",
  fontSize: 0.055
});

container.add(text);
scene.add(container);

// In your render loop, before rendering the scene
function animate() {
  ThreeMeshUI.update();
  renderer.render(scene, camera);
}
```

### Font Files

To display text, you need to provide MSDF font files (`.json` and `.png`). You can use the provided `Roboto-msdf` files in the [examples/assets directory](https://github.com/felixmariotto/three-mesh-ui/tree/master/examples/assets), or [create your own](https://github.com/felixmariotto/three-mesh-ui/wiki/Creating-your-own-fonts).

## Import

### ES Modules (JSM)

#### NPM

```javascript
import ThreeMeshUI from 'three-mesh-ui';
```

#### HTML `<script>` tag

Use an import map to define the modules.

```html
<!-- Defines the import map -->
<script async src="https://unpkg.com/es-module-shims@1.3.6/dist/es-module-shims.js"></script>
<script type="importmap">
{
    "imports": {
        "three": "https://unpkg.com/three@0.144.0/build/three.module.js",
        "three-mesh-ui": "https://unpkg.com/three-mesh-ui@6.5.3/build/three-mesh-ui.module.js"
    }
}
</script>

<!-- Then we can code our app -->
<script type="module">
    import * as THREE from "three";
    import * as ThreeMeshUI from "three-mesh-ui";

    // code goes here ...
</script>
```
*You can use the minified version `three-mesh-ui.module.min.js` for production.*

### CommonJS / UMD (JS)

#### Node.js

```javascript
const ThreeMeshUI = require('three-mesh-ui');
```

#### HTML `<script>` tag

```html
<!-- Load three.js before three-mesh-ui -->
<script src="https://unpkg.com/three@0.144.0/build/three.js"></script>
<script src="https://unpkg.com/three-mesh-ui@6.5.3/build/three-mesh-ui.js"></script>

<!-- Then we can code our app -->
<script>
    /* global THREE, ThreeMeshUI */
    // code goes here ...
</script>
```
*You can use the minified version `three-mesh-ui.min.js` for production.*

## License

[MIT](https://github.com/felixmariotto/three-mesh-ui/blob/master/LICENSE)