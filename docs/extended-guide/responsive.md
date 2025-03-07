---
sidebar_position: 1
title: レスポンシブ対応を行う
---

本節では、省力化コンポーネントをレスポンシブ化する方法について説明します。

省力化コンポーネントが提供する部品は、画面幅に応じて入力フォームの幅が変わるといった基本的なレスポンシブ機能を搭載しています。ただし、ラベルの位置や選択肢の並び方を画面サイズに応じて変えたい、といった場合には何らかの対応が必要になります。

## レスポンシブ対応の省力化コンポーネント部品を作成する

本節では、与えられたレスポンシブ要件を実現するために、元の省力化コンポーネント部品をラップして新たにレスポンシブ対応の部品を作成する方法を紹介します。

例として、`AxInputText` をレスポンシブ化した `RaxInputText` を以下のように実装します。  
ここでは、「画面サイズによってラベルの位置が変わること」をレスポンシブ要件として定義しています。

```tsx
export const RaxInputText = (props: AxInputTextProps) => {
  // 画面サイズの取得
  const deviceType = useDeviceType();
  // 画面サイズからラベル位置を決定する
  const labelPlacement = deviceType === "mobile" ? "top" : "left";
  // 元の部品を呼び出す
  return <AxInputText labelPlacement={labelPlacement} {...props} />;
};
```

利用方法は通常の `AxInputText` と同じです。今回、 `RaxInputText` は画面サイズに応じてラベル位置が変わるので、`labelPlacement` の指定はしません。

```tsx
return (
  <>
    <Row>
      <Col span={20} offset={1}>
        // highlight-next-line
        <AxInputText labelPlacement="left" item={view.normalItem} />
      </Col>
    </Row>
    <Row style={{ marginTop: "20px" }}>
      <Col span={20} offset={1}>
        // highlight-next-line
        <RaxInputText item={view.responsiveItem} />
      </Col>
    </Row>
  </>
);
```

`AxInputText` と `RaxInputText` の動作はそれぞれ以下のようになります。

![部品のレスポンシブ化](/../static/img/responisive-item.gif)

:::info
画面サイズを取得する方法は様々ありますが、 UI ライブラリが専用のフックを提供している場合があります。  
今回は、Ant Design が提供する `useBreakPoint` というフックを利用して画面サイズの取得を行い、画面サイズに応じてデバイスの種類を返すカスタムフック `useDeviceType()` を実装しています。

<details>
  <summary>`useDeviceType` の実装を見る</summary>

```tsx
import { Grid } from "antd";

/**
 * デバイスタイプを取得するフック
 *
 * @returns デバイスタイプ ("mobile" | "tablet" | "pc")
 */
export const useDeviceType = (): DeviceType => {
  const { useBreakpoint } = Grid;
  const screens = useBreakpoint();

  if (screens.lg) {
    // 992px <= 画面幅
    return "pc";
  }
  if (screens.sm) {
    // 576px <= 画面幅 < 992px
    return "tablet";
  }
  if (screens.xs) {
    // 画面幅 < 576px
    return "mobile";
  }
  // 画面幅が取得できない場合はモバイル端末として扱う
  return "mobile";
};
```

</details>
:::

## 画面全体をレスポンシブ化する

:::warning
画面全体をレスポンシブ化する場合、省力化コンポーネント以外への対応も必要となります。今回は Ant Design の機能を使って画面全体をレスポンシブ化する 1 例を紹介しますので、さらに詳しく知りたい場合は、お使いの UI ライブラリのドキュメントを参照してください。
:::

Ant Design の Grid システムと、先ほど作った `RaxInputText` を合わせると、画面全体のレスポンシブ対応が実現できます。

```tsx
<Row>
  <Col xs={20} sm={20} md={10} offset={1} style={{ marginTop: "10px" }}>
    <RaxInputText item={view.item1} />
  </Col>
  <Col xs={20} sm={20} md={10} offset={1} style={{ marginTop: "10px" }}>
    <RaxInputText item={view.item2} />
  </Col>
</Row>
<Row>
  <Col xs={20} sm={20} md={10} offset={1} style={{ marginTop: "10px" }}>
    <RaxInputText item={view.item3} />
  </Col>
  <Col xs={20} sm={20} md={10} offset={1} style={{ marginTop: "10px" }}>
    <RaxInputText item={view.item4} />
  </Col>
</Row>
```

![画面のレスポンシブ化](/../static/img/responisive-screen.gif)
