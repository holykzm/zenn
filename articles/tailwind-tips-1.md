---
title: "そもそもモバイルでは[ hover:~ ]が効かないように設定する"
emoji: "👆"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["tailwindcss","レスポンシブ"]
published: true
---

# TL;DR

```diff
// tailwind.config.ts

 /** @type {import('tailwindcss').Config} */
 module.exports = {
+  future: {
+    hoverOnlyWhenSupported: true,
+  },
 
   // other config
 }
```

# モバイルではホバーが残る

`hover:opacity-50`とした時、モバイルでその要素を軽く触れるとホバーが効いてしまう。
これはスクロールしている時に気になって眠れなくなるので、
`md:hover:opacity-50 max-md:active:opacity-50`みたいに書いていた🤮

# Tailwind側でも準備中

この問題はTailwindCSS側でも認識していて、将来的に対応するらしい。
それまでは `hoverOnlyWhenSupported` が用意されていて、モバイルでは `hover` を無効にしてくれるので、モバイルでの記述`active:`を足せばいい。

```diff
// tailwind.config.ts

 /** @type {import('tailwindcss').Config} */
 module.exports = {
+  future: {
+    hoverOnlyWhenSupported: true,
+  },
 
   // other config
 }
```

```diff
// Example

 <div 
-  className="bg-gray-200 hover:bg-black "
+  className="bg-gray-200 hover:bg-black active:bg-black "
   ></div>
```

# ビフォーアフター

**何もしない**
`hover:bg-black`がモバイルでも効いていてスクロールが終わっても黒いまま（ホバーが効いている）。
![hoverあり](/images/tailwind-tips/1/1.gif)

**futureを設定**
`hoverOnlyWhenSupported`を`true`にするとモバイルでは`hover`自体が効かなくなる。
![hoverOnlyWhenSupportedあり](/images/tailwind-tips/1/2.gif)

**モバイル対応**
モバイル用に`active:bg-black`を追加することでモバイルでは触れた時だけ黒くなる（アクションが効く）。
![activeあり](/images/tailwind-tips/1/3.gif)

---
**参考:**
[Configure Touch Screen Media Queries Using Tailwind CSS](https://www.getfishtank.com/blog/tailwind-css-for-touch-screen-media-queries)
[Solving the sticky hover effect on Mobile with TailwindCSS](https://dev.to/truongductri01/solving-the-sticky-hover-effect-on-mobile-with-tailwindcss-i5p)