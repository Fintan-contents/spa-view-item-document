---
sidebar_position: 1
title: useCsSelectNumberBoxItem
---

`useCsSelectNumberBoxItem` は、数値セレクトボックスに対応する Item を初期化するためのフックです。

## シグネチャ

<h3>`useCsSelectNumberBoxItem(label, state, rule, selOpt?, readonly?, placeholder?): CsSelectNumberBoxItem`</h3>

## 引数

| 引数名      | 必須 | 型                           | 説明                                                                                                                                                           |
| ----------- | ---- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label       | 〇   | `string`                     | 入力項目のラベルを指定します。                                                                                                                                 |
| state       | 〇   | `StateResult<number>*¹`      | 入力項目の状態変数を指定します。[useInit](../helper-function/useInit.md) を使用して初期化した状態変数を指定します。                                            |
| rule        | 〇   | `NumberValidationRule*²`     | 入力項目のバリデーションルールを指定します。[numberRule](../helper-function/numberRule.md)を使用して初期化したルールを指定します。                             |
| selOpt      |      | `SelectOptions`              | セレクトボックスの選択肢を指定します。[selectOptions](../helper-function/selectOptions.md) を使用して初期値を指定します。                                                                                                                         |
| readonly    |      | `RW.Editable \| RW.Readonly` | 入力項目が読み取り専用かどうかを指定します。`RW.Editable` は読み取り・書き込み可能、`RW.Readonly`は読み取り専用を表す値です。デフォルトは `RW.Editable` です。 |
| placeholder |      | `string`                     | プレースホルダーを指定します。                                                                                                                                 |

\*1：`StateResult`は `useState` の戻り値を管理する型定義です。詳しくは[useInit](../helper-function/useInit.md)を参照してください。

\*2：`NumberValidationRule`は`number`型のバリデーション定義情報（必須項目かどうか、最小・最大値、カスタムルール名など）を保持する型定義です。

## 返り値

引数で定義した初期値やバリデーションルール、選択肢など、数値セレクトボックス項目に関する情報が集約された `CsSelectNumberBoxItem` クラスのインスタンスを返します。

## 使用例

```tsx
useCsView({
  // highlight-start
  colSize: useCsSelectNumberBoxItem(
    "表示列数",
    useInit(2),
    numberRule(false),
    selectOptionNumbers([1, 2, 3, 4, 6]),
    RW.Editable,
    "列数を選択してください"
  ),
  // highlight-end
});
```
