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

Reactが見据える大規模開発とアーキテクチャ

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

# 今日のテーマ: Reactチームが見てる世界

大規模開発を支えるReactチームが見てる世界を、歴史から紐解く

1. ~~Reactの誕生~~
1. ReactとGraphQL
1. React Server Components

---
layout: section
---

# ReactとGraphQL

Metaを支える技術基盤

---

# 前提: Metaの大規模開発

Metaの開発は世界有数の規模

- 異次元な基盤と予算
  - 世界中に独自のデータセンターを配置
  - 海底ケーブルもGoogleと共同で保持
  - フレームワークや言語開発も厭わない開発予算
- 超大規模React開発
  - 数万〜10万のコンポーネントを保有
  - 多くの修正をCode modで自動化して保守

彼らは特に<span v-mark.underline.red class="font-bold">スケーラビリティ</span>を非常に重要視している

<!--
参考: https://medium.com/@syedmahmad/react-relay-modern-simplified-956f33739f0
-->

---

# MetaにとってのGraphQL

Reactと併用する技術であり、通信の課題を解決する技術

- MetaにとってのGraphQLはBFFに対する通信の課題を解決する技術
- Meta以外では**バックエンド通信のプロトコル**として採用されることが多い

開発元のMetaと世間では、<span v-mark.underline.red class="font-bold">GraphQL採用のモチベーションが異なる</span>ことが多い

---

# Metaの考えるGraphQLが担う層

<div class="flex justify-center mt-10">
  <img src="/graphql.png" alt="GraphQL" width="80%">
</div>

<!--
https://excalidraw.com/#json=J6xbE-rC2K5hIMY3EUYwW,HHuYJ-TUkRoT8SBc5xmBbw
-->

---
transition: fade
---

# MetaにとってのGraphQLとReact

Metaの大規模プロダクトたちを支えるアーキテクチャ

- MetaにとってReactとGraphQLは大規模システムを支える<span v-mark.underline.red class="font-bold">自律分散的アーキテクチャ</span>の基盤である
  - Not 中央集権アーキテクチャ（e.g. ReduxやWeb MVCなど）
  - [Thinking in Relay](https://relay.dev/docs/principles-and-architecture/thinking-in-relay/)などからもMetaの思考が読み取れる

---
transition: fade
---

# MetaにとってのGraphQLとReact

<div class="flex justify-center mt-10">
  <img src="/top-level-data-fetching.png" alt="Top Level Data Fetching">
</div>

---

# MetaにとってのGraphQLとReact

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

- MetaにとってReactとGraphQLは<span v-mark.underline.red class="font-bold">自立分散的アーキテクチャ</span>を構築するための基盤
  - コンポーネントが必要なデータを自分で宣言する世界
  - 現在もMetaで多くのプロダクトを支えている

---
layout: section
---

# React Server Components

新たな自立分散的アーキテクチャ

---

# React Server Components

React単体で前述の世界観を実現可能に

```tsx
// Server Component: Serverでのみ実行されるComponent
export async function Post({ id }: Props) {
  const post = await getPost(id);

  // ...
}

// Server Function: ClientからServerの関数を呼び出せるFunction
export async function updatePost(post: Partial<Post>) {
  "use server";

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

# まとめ

Reactは大規模開発に通用する

- Reactは大規模開発向けフレームワークで（も）ある
- MetaはReact+GraphQLで自立分散的なアーキテクチャを採用している
- React Server Componentsもまた自立分散的アーキテクチャであり、React+GraphQLの正当後継

---
layout: section
---

# End
