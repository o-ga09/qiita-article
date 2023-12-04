---
title: Re ： 1からはじめるSvelte入門【part 2】
tags:
  - Web
  - フロントエンド
  - Svelte
  - SvelteKit
  - Tutoial
private: false
updated_at: ""
id: null
organization_url_name: null
slide: false
ignorePublish: true
---

# はじめに

本記事は、svelte 初心者が一から入門して、Web アプリを１人で構築できるようになるためのハンズオン形式の投稿です。

# 想定読者

:::note warn

以下の知識がある前提で進めていきます。

- HTML、CSS が分かること
- バックエンドは解説しないので、何かしらの言語でバックエンドの処理を書けること
- Node.js の環境があること

:::

- バックエンドエンジニアだけど、フロントエンドは苦手な方
- Web エンジニアを目指す方
- Svelete に興味を持った方

# 環境

開発環境は、以下の想定で進めていきます。

- OS :
  - ProductVersion : 14.0
  - BuildVersion : 23A344
- Node.js : v18.16.1
- npm : 9.5.1
- Svelte : 4.0.5

# 参考リポジトリ

https://github.com/o-ga09/tutorial-Svelte/commits/

part 毎のソースコードをタグで作成しておりますので、part 毎のソースコードが必要な方はダウンロードしてご使用ください。

# 第 2 回目

## カウンターアプリ

### 想定作業時間

30 分

### 成果物

![スクリーンショット 2023-12-04 23.30.09.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1312905/ff731ab2-76c3-ea53-208f-b0ebf27c417c.png)

### 使用する構成

- Svelte
- SvelteKit
- TailwindCSS

## 手順解説

<details><summary>解説を見る</summary>

1 . Tailwind 導入

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

```diff_javascript:tailwind.config.js
/** @type {import('tailwindcss').Config} */
export default {
- content: [],
+ content: ['./src/**/*.{html,js,svelte,ts}'],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

```css:app.css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```diff_html:layout.svelte
<script>
	import './styles.css';
+	import '../app.css';
</script>

<div class="app">
	<main>
		<slot />
	</main>
</div>

<style>
	/* root layout style */
	main {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100vh;
	}
</style>

```

<br>

2 . +page.svelte 修正

```html:+page.svelte
<script>
	let count = 0;

	const plusButton = () => {
		count = count + 1;
	};

	const minusButton = () => {
		count = count - 1;
	};
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="counter">
	<h1 class="text-center">カウンターアプリ</h1>
	<div
		class="
		flex
		items-center
		justify-center
		w-64
		h-96
		text-5xl
		font-bold
		bg-lime-400
		rounded-lg
		m-4
	  "
	>
		{count}
	</div>
	<div class="flex items-center justify-center h-20">
		<button
			class="
		  h-full
		  w-20
		  m-4
		  bg-cyan-400
		  border-cyan-400
		  rounded-lg
		  text-3xl
		"
			on:click={plusButton}
		>
			+
		</button>
		<button
			class="
		  h-full
		  w-20
		  m-4
		  bg-cyan-400
		  border-cyan-400
		  rounded-lg
		  text-3xl
		"
			on:click={minusButton}
		>
			-
		</button>
	</div>
</div>

```

上記のように、Svelte では、`<Button>`タグに`on:click`などの特別なプロパティ
が最初からついています。
また、カウントの変数も React のように`useState`のような特別な関数を使用しなくても、
ただ、`let count = 1`でカウンターアプリを実装できてしまいます。

:::note info

今回の記事におけるポイントは、`<button on:click={}>`の使い方と、Svelte における状態を表す変数の使い方をマスターしました。

:::

</details>

# まとめ

いかがだったでしょうか？これから、私自身、Svelte を使用して Web アプリ構築するために本記事を投稿していこうと考えております。
よろしければ、いいね、フォローよろしくお願いいたします。

一緒に、Svelte について学んでいきましょう！

## 前回の記事はこちら

https://qiita.com/o-ga/items/6de543a495770a51956f
