---
sidebar_position: 1
title: レスポンシブ対応を行う
---

本節では、省力化コンポーネントおよび画面内の項目配置をレスポンシブ化する方法について紹介します。

省力化コンポーネントが提供する部品は、画面幅に応じて入力フォームの幅が変わる、といった基本的なレスポンシブ機能を搭載しています。ただし、ラベルの位置や選択肢の並び方を画面サイズに応じて自動で変えるような機能は標準で備わっていません。そのため、標準機能では満たせないレスポンシブ要件を実現するためには、省力化コンポーネントを拡張する必要があります。本節では、その一例を紹介します。

また、画面内の各項目（各省力化コンポーネント部品）の配置を画面サイズに応じて変えるためには、画面側でもレスポンシブ対応を行う必要があります。本節では、Ant Design を使用する場合の、項目の配置をレスポンシブ化する方法についても紹介します。

## レスポンシブ対応の省力化コンポーネント部品を作成する

本項では、レスポンシブ対応の省力化コンポーネント部品を作成する方法として、元の省力化コンポーネント部品をラップして拡張する方法を紹介します。  
ここでは、「画面サイズによってラベルの位置が変わること」をレスポンシブ要件として定義します。

テキスト入力用部品の `AxInputText` をレスポンシブ化した `RaxInputText` のコード例を以下に示します。  
`RaxInputText` の処理内容は次の 3 つです。

1. 現在の画面サイズを取得する
2. 画面サイズより、ラベルの位置を決定する
3. ラベル位置を設定して、 `AxInputText` を呼び出す

```tsx
/**
 * RaxInputTextのProps定義
 *  ※ AxInputTextのProps定義からlabelPlacementを除外する
 */
type RaxInputTextProps = Omit<AxInputTextProps, "labelPlacement">;

/** レスポンシブ対応版AxInputText */
export const RaxInputText = (props: RaxInputTextProps) => {
  // 1. 画面サイズの取得
  const deviceType = useDeviceType();
  // 2. ラベル位置の決定
  const labelPlacement = deviceType === "mobile" ? "top" : "left";
  // 3. 元部品の呼び出し
  return <AxInputText labelPlacement={labelPlacement} {...props} />;
};
```

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

利用方法は通常の `AxInputText` と同じです。今回、 `RaxInputText` は画面サイズに応じてラベル位置が変わるので、`labelPlacement` の指定はありません。

```tsx
return (
  <>
    <Row>
      <Col span={20} offset={1}>
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

## 項目の配置をレスポンシブ化する

:::warning
ここでは、 Ant Design の機能を使った項目配置のレスポンシブ化について紹介します。さらに詳しく知りたい場合は、お使いの UI ライブラリのドキュメントを参照してください。
:::

Ant Design の Grid システムでは、 `<Row />` （行を確保するための部品）と `<Col />` （列を確保するための部品）を組み合わせることで、領域を柔軟に分割することができます。また、 `<Col />` には、Ant Design が定義する幅空間ごとに領域幅を設定することができ、画面幅に応じて領域幅を切り替えることが可能です。

以下に示すコードは、4 つの入力項目の配置とラベル位置を画面幅に応じて変える際の実装例になります。

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

- `<Col xs={20} sm={20} md={10}` の部分で、項目の表示領域を画面幅に応じて変更させます。

  - `xs`, `sm`, `md` は幅空間ごとに領域幅を設定をするための Props で、例えば画面幅 `0px ~ 576px` の時には `xs` に指定した領域幅が適用されます。
  - 値には、最大数を 24 として領域幅を相対的に指定します。例えば 12 を指定すると、画面の横半分が領域として適用されます。

- `RaxInputText` を用いることで、ラベル位置を画面幅に応じて変更させます。

動作は以下のようになります。画面幅が広い時には項目は 2 列に並び、画面幅が狭くなると 1 列になります。また、ラベル位置も画面幅によって横配置と縦配置が切り替わります。

![画面のレスポンシブ化](/../static/img/responisive-screen.gif)
