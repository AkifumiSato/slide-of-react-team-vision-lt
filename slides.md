---
theme: default
# https://unsplash.com/ja/%E5%86%99%E7%9C%9F/%E6%97%A5%E9%A3%9F%E3%81%AE%E3%83%87%E3%82%B8%E3%82%BF%E3%83%AB%E5%A3%81%E7%B4%99-_ok8uVzL2gI
background: /background.png
class: text-center
highlighter: shiki
lineNumbers: false
colorSchema: "dark"
drawings:
  persist: false
transition: slide-left
title: Reactチームが見てる世界
mdc: true
---

# Reactチームが見てる世界

in ~~React Tokyo~~

Metaに学ぶ大規模フロントエンドのアーキテクチャ

---

# Profile

<div class="pb-5">
  <img src="https://avatars.githubusercontent.com/u/25711332?v=4" width="100" height="100">
</div>

```jsonc
// profile.jsonc
{
  "name": "佐藤 昭文",
  "alias": ["akfm_sato", "あっきー"],
  "job": "フロントエンドエキスパート",
  "tags": ["Next.js", "React", "Test", "リーン開発"],
  "sns": {
    "x": "akfm_sato",
    "GitHub": "AkifumiSato",
    "zenn.dev": "akfm",
  },
}
```

---

# Theme: アーキテクチャで見るReactの進化論

Metaで採用されてるアーキテクチャとその進化

1. React+GraphQL
1. React Server Components

※React Server Components: React界隈でデファクトとなりつつある仕様規約

---
layout: section
---

# ReactとGraphQL

現在もMetaを支える技術基盤

---

# Metaの大規模開発

Metaの開発は世界有数の規模

- 豊富な開発予算
  - フレームワークや言語開発
  - 独自のデータセンターや海底ケーブル
- 超大規模React開発
  - 数万〜10万のコンポーネントを保有

彼らは特に<span v-mark.underline.red class="font-bold">スケーラビリティ</span>を非常に重要視している

<!--
参考: https://medium.com/@syedmahmad/react-relay-modern-simplified-956f33739f0
-->

---

# MetaにとってのReactとGraphQL

ReactとGraphQLは併用する技術

- React: フロントエンドの課題を解決
- GraphQL: BFFに対する通信の課題を解決

---

# Metaの考えるGraphQLが担う層

<div class="flex justify-center mt-10">
  <img src="/graphql.png" alt="GraphQL" width="80%">
</div>

<!--
https://excalidraw.com/#json=J6xbE-rC2K5hIMY3EUYwW,HHuYJ-TUkRoT8SBc5xmBbw
-->

---

# GraphQLが解決しようとしていた課題

設計と通信効率のジレンマ

- 設計観点ではコンポーネント単位でデータフェッチしたい -> HTTP通信しすぎてすぐに劣化
- 通信効率観点では親コンポーネントで1回だけデータフェッチしたい -> God APIになって破綻

---

# GodAPIパターン

<div class="flex justify-center mt-10">
  <img src="/top-level-data-fetching.png" alt="Top Level Data Fetching">
</div>

---
layout: fact
---

## GraphQLは<br>設計と通信効率のジレンマを解決する技術

---

# GraphQL Co-Location

<div class="flex justify-center mt-10">
  <img src="/graphql-co-location.png" alt="GraphQL">
</div>

---

# GraphQL Co-Location

https://relay.dev/docs/tutorial/fragments-1/

```tsx
const PostFragment = graphql`
  fragment PostFragment on Post {
    title
    summary
    createdAt
  }
`;

export default function Post({ post }: Props) {
  const data = useFragment(PostFragment, post);

  // ...
}
```

- コンポーネントが必要なデータをコンポーネントの近くで宣言することで凝集性を高める
- GraphQLがデータフェッチを1つにまとめることで効率的なデータフェッチを実現

---

# ReactとGraphQL まとめ

Metaを支える技術基盤

- GraphQLは<span v-mark.underline.red class="font-bold">設計と通信効率のジレンマ</span>を解決する技術
- ReactとGraphQLを併用することで、大規模開発でもスケールするアーキテクチャを実現

---
layout: section
---

# React Server Components

現在主流なフロントエンドのアーキテクチャ

---

# React Server Components

React単体で前述の世界観を実現可能に

```tsx
// Server Component: Serverでのみ実行されるComponent
export async function Post({ id }: Props) {
  const post = await getPost(id);

  // ...
}
```

- 従来のReact+GraphQLの世界観の正当でシンプルな後継
- 最もサポートが進んで安定してるのはNext.js（App Router）

---
transition: fade
---

# RSCでのData Fetching

<div class="flex justify-center mt-10">
  <img src="/graphql-co-location.png" alt="GraphQL">
</div>

---

# RSCでのData Fetching

<div class="flex justify-center mt-10">
  <img src="/react-server-components.png" alt="React Server Components">
</div>

---

# React Server Componentsまとめ

React Server Components=スケーラブルなフロントエンドのアーキテクチャ

- React+GraphQLは設計と通信効率のジレンマを解決した
- React Server ComponentsはReact+GraphQLの正当後継

---
layout: section
---

# End
