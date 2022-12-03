---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: "text-center"
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS
css: unocss
---

# Next チュートリアルで覚える Nuxt3

<div class="flex justify-center items-center"><p class="ml-1 text-gray-400">ushironoko</p></div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
</div>

---

# 自己紹介

<img class="rounded-full border border-1" width="120" height="120" src="https://pbs.twimg.com/profile_images/1587289049848745986/zb3TbVvf_400x400.jpg" />

<br>

- 📝 **name** - ushironoko
- <carbon-logo-github /> **GitHub** - ushironoko
- <carbon-logo-twitter /> **Twitter** - @ushiro_noko
- 🖋️ **Blog** - ushironoko.me
- 🛠️ **Works** - STORES, inc. & NuxtLabs Japan by ZEN Advisor

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# 目次

- Next チュートリアルとは
- Nuxt3 とは
- 本日のゴール
- 実践

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Next チュートリアルとは

### Next.js Learn

https://nextjs.org/learn/basics/create-nextjs-app

- Next.js 公式のチュートリアル
- Next.js のさまざまな基本機能を一通り触りながら覚えられる
- 最終的に Vercel へ自作の markdown ベースブログをデプロイできる

<img class="absolute top-20 right-10" width="300" src="https://i.gyazo.com/61250d9085160648624d1777f97a5e3c.png" />

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Nuxt3 とは

https://nuxt.com/

- Nuxt.js の最新版
- Vue のフル機能をサポート
- ファイルベースルーティング、ページ毎の CSR/SSR/SSG/ISR(G)
- Vite or Webpack5
- esbuild transpiling
- Zero-Config TypeScript Support
- Node.js/Deno/Edge Functions/Worker などさまざまな環境で動作する
- auto-imports,特定ディレクトリ配下の d.ts の自動生成
- やっと出た(beta から 1 年)

<img class="absolute top-20 right-10" width="300" src="https://i.gyazo.com/1e0f92dba3bf0ae3e309b07722775184.png" />

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# 本日のゴール

https://nuxt.com/

- Next チュートリアルを実践形式で Nuxt に置き換えながら見せます
- Vercel…ではなく Cloudflare Pages へデプロイ(推しなので)
- 時間の都合で一部簡略化します

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

<p class="text-[100px] absolute top-20 left-94">実演</p>

<p class="text-[16px] absolute top-44 left-97">コードはコピペできます</p>
<img class="absolute bottom-4 left-60" src="https://i.gyazo.com/d7296f933a58946da37d4635955ab702.png" width="500" />

---

# プロジェクト生成&インストール

1. `nuxi` コマンドでスキャフォールド。

```shell
npx nuxi init pwa-night-ushironoko-demo
```

2. 移動

```shell
cd pwa-night-ushironoko-demo
```

3. 依存のインストール

```shell
yarn install
```

4. サーバー起動

```shell
yarn dev
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# 構成の確認

- `.nuxt`: 自動生成した型や、サーバーの起動に必要な情報などが格納される
- `app.vue`: エントリーポイントとなるコンポーネント
- `nuxt.config.ts`: Nuxt の設定を記述するファイル
- `tsconfig.json`: `.nuxt` 配下の `tsconfig.json` を extend している

## ポイント

- `.nuxt` 配下の型情報を用いて auto imports の型を効かせる
- `.nuxt` を再生成するときは `yarn postinstall`

<img class="absolute top-5 right-10" width="260" src="https://i.gyazo.com/0abf7375639c8b48da84bee71bd3fad2.png" />

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# pages/index.vue を作る

1. `app.vue` を消す
2. `pages/index.vue` を作る

pages/index.vue

```vue
<template>
  <h1>First post</h1>
</template>
```

<br>

### ポイント

- `app.vue` か `pages/index.vue` をエントリーポイントにする
  - 単一のページ(LP など)は `app.vue`、そうでない場合は `pages/index.vue`
  - `app.vue` を使うとバンドルから `vue-router` が除外される

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# pages/posts/first_post.vue を作る

1. `pages/posts/first_post.vue` を作る
2. `pages/index.vue` を編集する

pages/posts/first_post.vue

```vue
<template>
  <h1>First post</h1>
  <h2><NuxtLink href="/">Back to home</NuxtLink></h2>
</template>
```

pages/index.vue

```vue
<template>
  <h1>Read <NuxtLink href="/posts/first-post">this page!</NuxtLink></h1>
</template>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

1. `public` ディレクトリを作って `public/images/profile.jpeg` を置く
2. `components/ProfileImage.vue` を作る
3. `pages/posts/first_post.vue` の title を修正する

components/ProfileImage.vue

```vue
<template>
  <img src="/images/profile.jpeg" height="144" width="144" alt="ushironoko" />
</template>
```

pages/posts/first_post.vue

```vue
<template>
  <Head>
    <title>First Post</title>
  </Head>
  <h1>First post</h1>
  <h2><NuxtLink href="/">Back to home</NuxtLink></h2>
</template>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

1. `public` ディレクトリを作って `public/images/profile.jpeg` を置く
2. `components/ProfileImage.vue` を作る
3. `pages/posts/first_post.vue` の title を修正する

<br>

### ポイント

- Image Optimize したい場合は https://v1.image.nuxtjs.org/ で(今回は時間都合で省略)

<img class="absolute top-74 left-14" width="430" src="https://i.gyazo.com/2af86ff2c5c64821616d4e61f787be66.png" />

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

4. サードパーティ JS を読み込む(時間がないのでスキップ！)

pages/posts/first_post.vue

```vue
<script setup lang="ts">
const handleOnLoad = () =>
  console.log(`script loaded correctly, window.FB has been populated`);
useHead({
  script: [
    {
      src: "https://connect.facebook.net/en_US/sdk.js",
      defer: true,
      onload: handleOnLoad,
    },
  ],
});
</script>

<template>
  <Head>
    <title>First Post</title>
  </Head>

  <h1>First post</h1>
  <h2><NuxtLink href="/">Back to home</NuxtLink></h2>
</template>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

5. `sass` をインストールする
6. `layouts/default.vue` を作る

```shell
yarn add -D sass
```

layouts/default.vue

```vue
<template>
  <div class="container">
    <slot />
  </div>
</template>

<style lang="scss" scoped>
.container {
  max-width: 36rem;
  padding: 0 1rem;
  margin: 3rem auto 6rem;
}
.header {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.backToHome {
  margin: 3rem 0 0;
}
</style>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

7. `assets/styles/global.scss` を作る

assets/styles/global.scss

```scss
html,
body {
  padding: 0;
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu,
    Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
  line-height: 1.6;
  font-size: 18px;
}

* {
  box-sizing: border-box;
}

a {
  color: #0070f3;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

img {
  max-width: 100%;
  display: block;
}

p {
  margin: 0;
}
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

8. `assets/styles/global.scss` を登録する

nuxt.config.ts

```ts
export default defineNuxtConfig({
  css: ["~/assets/styles/global.scss"],
});
```

<br>

### ポイント

- `layouts/default.vue` がデフォルトで全てのページに適用される
  - 別途指定する場合は `definePageMeta` で指定する
- グローバル css は `nuxt.config.ts` で登録する
  - layouts で scoped style を使っている場合そのレイアウト以外では適用されないため

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

9. `assets/styles/utils.scss` を作る

```scss
.heading2Xl {
  font-size: 2.5rem;
  line-height: 1.2;
  font-weight: 800;
  letter-spacing: -0.05rem;
  margin: 1rem 0;
}

.headingXl {
  font-size: 2rem;
  line-height: 1.3;
  font-weight: 800;
  letter-spacing: -0.05rem;
  margin: 1rem 0;
}

.headingLg {
  font-size: 1.5rem;
  line-height: 1.4;
  margin: 1rem 0;
}

.headingMd {
  font-size: 1.2rem;
  line-height: 1.5;
}

.borderCircle {
  border-radius: 9999px;
}

.colorInherit {
  color: inherit;
}

.whitespace-pre-wrap {
  white-space: pre-wrap;
}
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

10. `layouts/default.vue` を編集する

```vue
<script setup lang="ts">
const name = "Ushironoko";
const siteTitle = "Learn how to build a personal website using Nuxt3";
</script>

<template>
  <div class="container">
    <Head>
      <Title>{{ siteTitle }}</Title>
      <Link rel="icon" href="/images/profile.jpeg" />
      <Meta
        name="description"
        content="Learn how to build a personal website using Next.js"
      />
      <Meta
        property="og:image"
        :content="`https://og-image.vercel.app/${encodeURI(
          siteTitle
        )}.png?theme=light&md=0&fontSize=75px&images=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Ffront%2Fassets%2Fdesign%2Fnextjs-black-logo.svg`"
      />
      <Meta name="og:title" :content="siteTitle" />
      <Meta name="twitter:card" content="summary_large_image" />
    </Head>
    <header class="header">
      <NuxtLink href="/">
        <img
          priority
          src="/images/profile.jpeg"
          class="borderCircle"
          height="144"
          width="144"
          alt=""
        />
      </NuxtLink>
      <h2 class="heading2Xl">
        <NuxtLink class="colorInherit" href="/">{{ name }}</NuxtLink>
      </h2>
    </header>
    <main><slot /></main>
    <div class="backToHome">
      <NuxtLink href="/">← Back to home</NuxtLink>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "~/assets/styles/utils.scss";

.container {
  max-width: 36rem;
  padding: 0 1rem;
  margin: 3rem auto 6rem;
}
.header {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.backToHome {
  margin: 3rem 0 0;
}
</style>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

11. `layouts/home.vue` を作る

```vue
<script setup lang="ts">
const name = "Ushironoko";
const siteTitle = "Learn how to build a personal website using Nuxt3";
</script>

<template>
  <div class="container">
    <Head>
      <Title>{{ siteTitle }}</Title>
      <Link rel="icon" href="/images/profile.jpeg" />
      <Meta
        name="description"
        content="Learn how to build a personal website using Next.js"
      />
      <Meta
        property="og:image"
        :content="`https://og-image.vercel.app/${encodeURI(
          siteTitle
        )}.png?theme=light&md=0&fontSize=75px&images=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Ffront%2Fassets%2Fdesign%2Fnextjs-black-logo.svg`"
      />
      <Meta name="og:title" :content="siteTitle" />
      <Meta name="twitter:card" content="summary_large_image" />
    </Head>
    <header class="header">
      <img
        priority
        src="/images/profile.jpeg"
        class="borderCircle"
        height="144"
        width="144"
        alt=""
      />
      <h1 class="heading2Xl">{{ name }}</h1>
    </header>
    <main><slot /></main>
  </div>
</template>

<style lang="scss" scoped>
@use "~/assets/styles/utils.scss";

.container {
  max-width: 36rem;
  padding: 0 1rem;
  margin: 3rem auto 6rem;
}
.header {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

10. `layouts/default.vue` を編集する
11. `layouts/home.vue` を作る

<br>

### ポイント

- 型付けしたい場合 https://github.com/Tahul/pinceau などの CSS-in-TS ライブラリを検討

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# assets,meta,css をセットする

12. `pages/index.vue` を編集する

```vue
<script setup lang="ts">
definePageMeta({
  layout: "home",
});
</script>

<template>
  <section class="headingMd">
    <p>こんにちは！</p>
    <p>
      (This is a sample website - you’ll be building a site like this on
      <a href="https://nuxt.com">Nuxt3</a>.)
    </p>
  </section>
</template>

<style lang="scss" scoped>
@use "~/assets/styles/utils.scss";
</style>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# data fetch & dynamic routes

- useFetch によるユニバーサルな fetch
- SSG モードでプリレンダリング

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# data fetch & dynamic routes

1. マークダウンファイルを用意する

`posts/pre-rendering.md`

```md
---
title: "Crawl-based Pre-rendering"
publishedAt: "2022-11-16"
---

Use the `nuxi generate` command to build your application.
For every page, Nuxt uses a crawler to generate a corresponding HTML and payload files.
The built files will be generated in the `.output/public` directory.
```

`posts/edge-rendering.md`

```md
---
title: "Rendering on CDN Edge Workers"
publishedAt: "2022-11-16"
---

Traditionally, server-side and universal rendering was only possible using Node.js. Nuxt 3 takes it to another level by directly rendering code in CDN edge workers, reducing latency and costs.
Nitro is the new server engine that powers Nuxt 3. It offers cross-platform support for Node.js, Deno, Workers, and more. Nitro's design is platform-agnostic and allows rendering a Nuxt application at the edge, closer to your users, allowing replication and further optimizations.
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# data fetch & dynamic routes

2. パーサーライブラリをインストールする
3. API を作る

```shell
yarn add -D gray-matter remark remark-html
```

`server/api/posts/sortedpostsData.ts`

```ts
import fs from "fs";
import path from "path";
import matter from "gray-matter";

const postsDirectory = path.join(process.cwd(), "posts");

export default defineEventHandler(() => {
  console.info(import.meta.url);
  const fileNames = fs.readdirSync(postsDirectory);
  const allPostsData = fileNames.flatMap((fileName) => {
    try {
      const id = fileName.replace(/\.md$/, "");
      const fullPath = path.join(postsDirectory, fileName);
      const fileContents = fs.readFileSync(fullPath, "utf8");
      const matterResult = matter(fileContents);

      return {
        id,
        ...matterResult.data,
      } as {
        id: string;
        title: string;
        description: string;
        publishedAt: string;
      };
    } catch (e) {
      console.error(e);
      return [];
    }
  });

  return allPostsData.sort(({ publishedAt: a }, { publishedAt: b }) => {
    if (a < b) {
      return 1;
    } else if (a > b) {
      return -1;
    } else {
      return 0;
    }
  });
});
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# data fetch & dynamic routes

2. パーサーライブラリをインストールする
3. API を作る

`server/api/posts/postsData.ts`

```ts
import fs from "fs";
import path from "path";
import matter from "gray-matter";
import { remark } from "remark";
import html from "remark-html";

const postsDirectory = path.join(process.cwd(), "posts");

export default defineEventHandler(async (event) => {
  const query = getQuery(event);
  const fullPath = path.join(postsDirectory, `${query.id}.md`);
  const fileContents = fs.readFileSync(fullPath, "utf8");

  const matterResult = matter(fileContents);

  const processedContent = await remark()
    .use(html)
    .process(matterResult.content);
  const contentHtml = processedContent.toString();

  return {
    id: query.id,
    contentHtml,
    ...matterResult.data,
  };
});
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# data fetch & dynamic routes

4. 動的ルートページを定義する

`pages/posts/[id].vue`

```vue
<script setup lang="ts">
const { params } = useRoute();

const id = Array.isArray(params.id) ? params.id[0] : params.id;

const { data } = useFetch(`/api/posts/postData?id=${encodeURIComponent(id)}`, {
  key: id,
});
</script>

<template>
  <div class="whitespace-pre-wrap" v-html="data?.contentHtml"></div>
</template>

<style lang="scss">
.whitespace-pre-wrap {
  white-space: pre-wrap;
}
</style>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# data fetch & dynamic routes

5. pages/index.vue を編集する

pages/index.vue

```vue
<script setup lang="ts">
definePageMeta({
  layout: "home",
});

const { data: posts } = useFetch("/api/posts/sortedpostsData");
</script>

<template>
  <div class="flex justify-center">
    <main>
      <section>
        <div v-for="post in posts" :key="post.id">
          <p>{{ post.publishedAt }}</p>
          <NuxtLink :href="`/posts/${post.id}`">
            <h2 class="headingLg">
              <p>{{ post.title }}</p>
            </h2>
          </NuxtLink>
        </div>
      </section>
    </main>
  </div>
</template>

<style lang="scss" scoped>
@use "~/assets/styles/utils.scss";
</style>
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# data fetch & dynamic routes

### ポイント

<br>

- API Routes(`server/api`) で api を定義
- `useFetch`で定義した api をコール
  - 一意になるキーを渡すことでキャッシュを回避
- `[id].vue`の形で動的ルートを定義
- `useRoute`でパラメータへアクセス

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Deploy on Cloudflare Pages

1. Cloudflare へログイン後、Pages から Git 連携
2. ビルドコマンドと環境変数を設定

ビルドコマンド

```shell
yarn generate
```

ビルド出力ディレクトリ

```shell
/.output/public
```

env name

```shell
NODE_VERSION
```

env value

```shell
v16.14.2
```

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Deploy on Cloudflare Pages

### ポイント

- API Routes で Node.js API を用いたため SSG が必要
  - Node.js API 互換のある環境なら SSR が可能(Deno Deploy 等)
- `useFetch`で取得する値はビルド時に json 化され、本番では NuxtLink によって Preload される

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# まとめ

- Nuxt3 では様々な機能が auto import できる
- 型の自動生成により、auto import された関数に型がつく
- レイアウト定義は`layout/`で、個別に指定する場合ページで`definePageMeta`
- css はローダーをインストールするだけでよしなに使えるようにしてくれる
- SSG ではビルド時に`usefetch`をモックして json 化し、Preload する
- 他にも `middleware`、`server middleware`、`plugins`、vitest ベースのテストランナー、多様なカスタムフックなど目玉機能が多数
- 続きは 👉 https://nuxt.com/docs/getting-started/introduction で

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

<p class="text-[100px] absolute top-40 left-110">終</p>
<a target="_blank" rel="noopener noreferrer" href="https://pwa-night-conference-2022.vercel.app/1" class="text-[16px] absolute top-70 left-60">スライドの公開先👉https://pwa-night-conference-2022-ushironoko.vercel.app/1</a>
<a target="_blank" rel="noopener noreferrer" href="https://github.com/ushironoko/next-tutorial-on-nuxt-3" class="text-[16px] absolute top-80 left-60">完成品👉 https://github.com/ushironoko/next-tutorial-on-nuxt-3</a>
<a target="_blank" rel="noopener noreferrer" href="https://sli.dev/" class="text-[16px] absolute top-90 left-60">powerd by👉 https://sli.dev/</a>

<style>
h1 {
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 50%);
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>
