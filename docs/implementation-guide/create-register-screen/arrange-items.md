---
sidebar_position: 4
title: 3. 入力項目を配置する
---

画面の定義が完了したら、画面コンポーネントを使用して入力項目を配置していきます。  

入力項目を配置する方法として、 `AxTableLayout` という画面コンポーネントを使用して自動で配置する方法と、一つ一つの入力項目に対応する画面コンポーネントを使用して手動で配置する方法の 2 つがあります。

:::note
省力化コンポーネントでは 、UI コンポーネントライブラリごとに専用の画面コンポーネントを提供しています。
それぞれの画面コンポーネントは、以下に示すプレフィックスによって分類されます。

| UI コンポーネントライブラリ | プレフィックス | 画面コンポーネント例 |
| --------------------------- | -------------- | -------------------- |
| Ant Design                  | `Ax`           | `AxInputText`        |
| Material UI                 | `Mx`           | `MxInputText`        |
| React Bootstrap             | `Bsx`          | `BsxInputText`       |

実装ガイドでは、Ant Design ( `Ax` から始まる部品) を例として記述しています。

:::

## 自動で入力項目を配置する

自動で入力項目を配置をする場合は、 `AxTableLayout` という画面コンポーネントを使用します。 `view` という Props に表示したい画面の View の変数を指定します。 `colSize` という Props に画面に並べる際の列数を指定します。

```tsx
// 対象画面の View を初期化する
const view = useRegisterUserView();
// AxTableLayoutに View を渡すことで入力項目を自動配置する
return <AxTableLayout view={view} colSize={2} />;
```

上記のように記述した場合、次のような画面が表示されます。

![入力項目の定義5個](/img/screen-item-5-2.png)

## 手動で入力項目を配置する

手動で入力項目を配置をする場合は、各入力項目の Item の型に応じた画面コンポーネントを使用します。 `item` という Props に対応する入力項目の Item の変数を指定します。

使用可能な画面コンポーネント一覧については、[リファレンス](../../category/リファレンス)を参照してください。

```tsx
// 対象画面の View を初期化する
const view = useRegisterUserView();
// 各画面コンポーネントに Item を渡すことで入力項目を手動配置する
return (
  <>
    <AxInputText item={view.userName} />
    <AxInputPassword item={view.password} />
    <AxRadioBox item={view.gender} />
    <AxInputDate item={view.birthDay} />
    <AxInputNumber item={view.terminalNum} />
  </>
);
```

上記のように記述した場合、次のような画面が表示されます。

![入力項目の定義5個](/img/screen-item-5.png)

:::info

- **自動配置のメリット**
  - 項目数が多くても、コードの記述量が増えない
  - `colSize` を変更することでレイアウトが簡単に変更できる
- **手動配置のメリット**
  - 複雑なレイアウトにも対応できる
  - 画面コンポーネントに `item` 以外の Props を渡すことができる
    :::
