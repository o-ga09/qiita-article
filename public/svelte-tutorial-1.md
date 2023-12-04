---
title: Re ： 1からはじめるSvelte入門【part 1】
tags:
  - Web
  - フロントエンド
  - Svelte
  - SvelteKit
  - Tutoial
private: false
updated_at: "2023-12-04T13:26:35+09:00"
id: 6de543a495770a51956f
organization_url_name: null
slide: false
ignorePublish: false
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

# やること

<font color="red">**最終目標**</font>は、AWS を使用したフロント＋バック＋認証付きの Web アプリを作成できるように
なること。

# 始める前に

## Svelte とは？

＞＞公式引用

> Svelte とは permalink
> 手短に言えば Svelte は、ナビゲーションバーやコメントセクション、コンタクトフォームなど、ユーザーがブラウザで見たり操作したりするユーザーインターフェースコンポーネントを書く方法です。Svelte コンパイラは、コンポーネントを、ページの HTML をレンダリングする実行可能な JavaScript と、ページのスタイリングをする CSS に変換します。このガイドの残りの部分を理解するのに Svelte を知っておく必要はありませんが、もし知っていれば役に立つでしょう。より詳しく知りたい場合は、Svelte のチュートリアル をご覧ください。

Web アプリを作る際に、必要な UI コンポーネントを作成するためのツール。

## SvelteKit とは？

＞＞公式引用

> SvelteKit は、Svelte を使用して堅牢でハイパフォーマンスな web アプリケーションを迅速に開発するためのフレームワークです。もしあなたが React 界隈から来たのであれば、SvelteKit は Next に似ているものです。Vue 界隈から来たのであれば、Nuxt に似ています。

公式にも記載のある通り、React というところの Next.js、Vue いうところの Nuxt.js にあたる Web フレームワークです。

## Svelte + SvelteKit を使用すると何がうれしいのか？

- Bundle サイズが小さい
- 少ない手間で効率的な Web アプリを構築できる
- ビルトインで色々な処理が書ける

# 第１回目

## 環境構築 + Hello World

### 想定作業時間

- 15 分

### 成果物

![スクリーンショット 2023-12-04 22.30.27.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1312905/d24b7b49-daf9-71bd-4ffe-d553a8b953ce.png)

### 使用する構成

- Svelte
- SvelteKit

## 手順解説

<details><summary>解説を見る</summary>

1 . Svelte プロジェクトを作成する

```bash
npm create svelte@latest [好きなプロジェクト名]
cd [プロジェクト名]
npm install
```

<br>

2 . 一度、公式が用意したサンプルが動作するか確認する

```bash
npm run dev
```

<br>

3 . 不要なファイル削除する

- about ディレクトリ
- sverdle ディレクトリ
- src/Counter.svelte

<br>

4 . Hello World を書く

```html:src/routes/+layout.svelte
<script>
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

```html:src/routes/+page.svelte
<script>
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<h1>Hello World !</h1>

<style>
	h1 {
		text-align: center;
	}
</style>
```

```css:src/styles.css
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Times New Roman', Times, serif;
	color: black;
}

```

</details>

# まとめ

いかがだったでしょうか？これから、私自身、Svelte を使用して Web アプリ構築するために本記事を投稿していこうと考えております。
よろしければ、いいね、フォローよろしくお願いいたします。

一緒に、Svelte について学んでいきましょう！
