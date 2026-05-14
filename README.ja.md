# three-mesh-ui

<p align="center">
  <a href="https://www.npmjs.com/package/three-mesh-ui">
    <img alt="NPM" src="https://img.shields.io/npm/v/three-mesh-ui.svg"/>
  </a>
  <a href="https://github.com/felixmariotto/three-mesh-ui/blob/master/LICENSE">
    <img alt="MIT License" src="https://img.shields.io/github/license/felixmariotto/three-mesh-ui"/>
  </a>
</p>

<p align="center">
  <a href="https://felixmariotto.github.io/three-mesh-ui/"><strong>ライブデモ</strong></a>
  &nbsp;|&nbsp;
  <a href="https://www.npmjs.com/package/three-mesh-ui"><strong>NPM</strong></a>
  &nbsp;|&nbsp;
  <a href="https://github.com/felixmariotto/three-mesh-ui/wiki"><strong>ドキュメント</strong></a>
  &nbsp;|&nbsp;
  <a href="https://github.com/felixmariotto/three-mesh-ui/wiki/Roadmap-&-Contributions"><strong>コントリビューション</strong></a>
</p>

📢 **v7.x.x は現在評価中です！** 最新の開発状況はこちらで確認できます: https://github.com/felixmariotto/three-mesh-ui/pull/223

<a href="https://three-mesh-ui.herokuapp.com/#interactive_button">
  <img alt="ホバーおよび選択状態を持つインタラクティブなボタン" target="_blank" src="https://felixmariotto.s3.eu-west-3.amazonaws.com/three-mesh-ui-teasers/buttons_opti.gif" width="45%">
</a>
<a href="https://three-mesh-ui.herokuapp.com/#hidden_overflow">
  <img alt="スクロールと hidden overflow（はみ出し部分の非表示）を備えたテキストパネル" target="_blank" src="https://felixmariotto.s3.eu-west-3.amazonaws.com/three-mesh-ui-teasers/hidden_overflow_opti.gif" width="45%">
</a>
<a href="https://three-mesh-ui.herokuapp.com/#nested_blocks">
  <img alt="ネストされたコンテナとテキスト配置による複雑なレイアウト" target="_blank" src="https://felixmariotto.s3.eu-west-3.amazonaws.com/three-mesh-ui-teasers/nested_layout_opti.gif" width="45%">
</a>
<a href="https://three-mesh-ui.herokuapp.com/#keyboard">
  <img alt="テキスト入力用のインタラクティブな3Dキーボード" target="_blank" src="https://felixmariotto.s3.eu-west-3.amazonaws.com/three-mesh-ui-teasers/keyboard_opti.gif" width="45%">
</a>

## これは何ですか？

**three-mesh-ui** は、VR/AR 体験におけるユーザーインターフェースを構築するためのライブラリです。[three.js](https://threejs.org) をベースに、three.js のために構築されています。

WebXR の没入型セッション（immersive session）では HTML/CSS を使用してユーザーインターフェースを作成することができないため、その問題を解決するべく本ライブラリは作成されました。UI 自体が `THREE.Object3D` のインスタンスとなる 3D UI を作成でき、任意の `THREE.Scene` にそのまま追加することが可能です。

これはフレームワークではなく、three.js 以外の依存関係を持たない最小限のライブラリです。

## 特徴

- **VR/AR 対応**: UI を `THREE.Object3D` インスタンスとして構築するため、没入型環境に最適です。
- **宣言的レイアウト**: `contentDirection`、`justifyContent`、`alignItems` などのプロパティを備えた Flexbox ライクなシステムを使用し、簡単かつ強力なレイアウトを実現します。
- **テキストとフォントのサポート**: MSDF（Multi-channel Signed Distance Field）フォントを使用して、鮮明なテキストをレンダリングします。ワードラップ（折り返し）、文字間隔（letter-spacing）、オーバーフロー制御をサポートしています。
- **インタラクティブなコンポーネント**: `Block`、`Text`、インタラクティブな `Keyboard` などのコアコンポーネントが含まれています。
- **スタイリング**: 角丸、ボーダー、不透明度を制御できる背景などを使用してコンポーネントをカスタマイズできます。

## クイックスタート

### すぐに試す

- **JSFiddle**: [こちらの JSFiddle でお試しください](https://jsfiddle.net/felixmariotto/y81rf5t2/44/)
- **react-three-fiber**: [始めるための CodeSandbox はこちらです](https://codesandbox.io/s/react-three-mesh-ui-forked-v7n0b?file=/src/index.js)

### インストール

```bash
npm install three-mesh-ui
```

⚠️ `three` は peer dependency（ピア依存関係）です。

### 基本的な使い方

```javascript
import * as THREE from 'three';
import ThreeMeshUI from 'three-mesh-ui';

// シーンの作成時
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

// レンダリングループ内（シーンをレンダリングする前）
function animate() {
  ThreeMeshUI.update();
  renderer.render(scene, camera);
}
```

### フォントファイル

テキストを表示するには、MSDF フォントファイル（`.json` と `.png`）を用意する必要があります。[examples/assets ディレクトリ](https://github.com/felixmariotto/three-mesh-ui/tree/master/examples/assets)に用意されている `Roboto-msdf` ファイルを使用するか、[独自のフォントを作成](https://github.com/felixmariotto/three-mesh-ui/wiki/Creating-your-own-fonts)することができます。

## インポート

### ES Modules (JSM)

#### NPM

```javascript
import ThreeMeshUI from 'three-mesh-ui';
```

#### HTML `<script>` タグ

インポートマップを使用してモジュールを定義します。

```html
<!-- インポートマップの定義 -->
<script async src="https://unpkg.com/es-module-shims@1.3.6/dist/es-module-shims.js"></script>
<script type="importmap">
{
    "imports": {
        "three": "https://unpkg.com/three@0.144.0/build/three.module.js",
        "three-mesh-ui": "https://unpkg.com/three-mesh-ui@6.5.3/build/three-mesh-ui.module.js"
    }
}
</script>

<!-- その後、アプリのコードを記述します -->
<script type="module">
    import * as THREE from "three";
    import * as ThreeMeshUI from "three-mesh-ui";

    // ここにコードを記述します ...
</script>
```
*本番環境では、縮小版の `three-mesh-ui.module.min.js` を使用できます。*

### CommonJS / UMD (JS)

#### Node.js

```javascript
const ThreeMeshUI = require('three-mesh-ui');
```

#### HTML `<script>` タグ

```html
<!-- three-mesh-ui の前に three.js を読み込みます -->
<script src="https://unpkg.com/three@0.144.0/build/three.js"></script>
<script src="https://unpkg.com/three-mesh-ui@6.5.3/build/three-mesh-ui.js"></script>

<!-- その後、アプリのコードを記述します -->
<script>
    /* global THREE, ThreeMeshUI */
    // ここにコードを記述します ...
</script>
```
*本番環境では、縮小版の `three-mesh-ui.min.js` を使用できます。*

## ライセンス

[MIT](https://github.com/felixmariotto/three-mesh-ui/blob/master/LICENSE)
