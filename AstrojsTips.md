## レスポンシブ対応に便利なAstro機能

**Picture コンポーネントで画像最適化:**
```astro
---
import { Picture } from 'astro:assets';
import myImage from '../assets/hero.jpg';
---

<Picture 
  src={myImage} 
  widths={[400, 800, 1200]} 
  sizes="(max-width: 768px) 100vw, (max-width: 1024px) 50vw, 800px"
  formats={['avif', 'webp']} 
  alt="Hero image"
/>
```

**ViewTransitions でスムーズなページ遷移:**
```astro
---
import { ViewTransitions } from 'astro:transitions';
---
<head>
  <ViewTransitions />
</head>
```

## パフォーマンス最適化

**コンポーネントの遅延読み込み:**
```astro
---
// 重いコンポーネントは条件付きでインポート
const HeavyComponent = await import('../components/Heavy.astro')
  .then(m => m.default);
---

<!-- client:visible で画面に入ったら読み込み -->
<HeavyComponent client:visible />
```

**Partytown でサードパーティスクリプト最適化:**
```astro
<script type="text/partytown" src="https://analytics.example.com/script.js"></script>
```

## 開発効率アップ

**Content Collections でブログ管理:**
```ts
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const blog = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    pubDate: z.date(),
    draft: z.boolean().default(false),
  }),
});
```

**環境変数の型安全な利用:**
```ts
/// <reference types="astro/client" />
interface ImportMetaEnv {
  readonly PUBLIC_API_URL: string;
  readonly SECRET_API_KEY: string;
}
```

## CSS管理のコツ

**scoped スタイルと global スタイルの使い分け:**
```astro
<style>
  /* コンポーネント内のみ適用 */
  h1 { color: blue; }
</style>

<style is:global>
  /* サイト全体に適用 */
  @media (max-width: 768px) {
    .mobile-hidden { display: none; }
  }
</style>
```

**CSS変数でテーマ管理:**
```astro
<style define:vars={{ primaryColor, spacing }}>
  .card {
    background: var(--primaryColor);
    padding: var(--spacing);
  }
</style>
```

## Islands Architecture の活用

```astro
<!-- 必要な時だけJSを読み込む -->
<Counter client:idle />        <!-- アイドル時 -->
<Search client:load />         <!-- 即座に -->
<Comments client:visible />    <!-- 表示時 -->
<Share client:media="(min-width: 768px)" /> <!-- メディアクエリ -->
```

## ビルド最適化

**astro.config.mjsの設定:**
```js
export default defineConfig({
  output: 'hybrid', // 静的+動的のハイブリッド
  prefetch: {
    prefetchAll: true // リンクの自動プリフェッチ
  },
  compressHTML: true, // HTML圧縮
  build: {
    inlineStylesheets: 'auto' // CSSインライン化
  }
});
```