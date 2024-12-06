---
sidebar_position: 1
title: useCsInputNumberRangeItem
---

`useCsInputNumberRangeItem` は、数値範囲入力ボックスに対応する Item を初期化するためのフックです。

## シグネチャ

<h3>`useCsInputNumberRangeItem(label, state, rule, readonly?, lowerPlaceholder?, upperPlaceholder?): CsInputNumberRangeItem`</h3>

## 引数

| 引数名           | 必須 | 型                           | 説明                                                                                                                                                              |
| ---------------- | ---- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label            | 〇   | `string`                     | 入力項目のラベルを指定します。                                                                                                                                    |
| state            | 〇   | `StateResult<number[]>*¹`    | 入力項目の状態変数を指定します。[useRangeInit](../helper-function/useRangeInit.md) を使用して初期化した状態変数を指定します。                                               |
| rule             | 〇   | `NumberValidationRule*²`     | 入力項目のバリデーションルールを指定します。[numberRule](../helper-function/numberRule.md)を使用して初期化したルールを指定します。                                |
| readonly         |      | `RW.Editable \| RW.Readonly` | 入力項目が読み取り専用かどうかを指定します。`RW.Editable` は読み取り・書き込み可能、`RW.Readonly`は読み取り専用を表す値です。デフォルトは `RW.Editable` です。 　 |
| lowerPlaceholder |      | `string`                     | 下限値のプレースホルダーを指定します。                                                                                                                            |
| upperPlaceholder |      | `string`                     | 上限値のプレースホルダーを指定します。                                                                                                                            |

\*1：`StateResult`は `useState` の戻り値を管理する型定義です。詳しくは[useRangeInit](../helper-function/useRangeInit.md)を参照してください。

\*2：`NumberValidationRule`は`number`型のバリデーション定義情報（必須項目かどうか、最小・最大値、カスタムルール名など）を保持する型定義です。

## 返り値

引数で定義した初期値やバリデーションルールなど、数値範囲入力項目に関する情報が集約された `CsInputNumberRangeItem` クラスのインスタンスを返します。

## 使用例

```tsx
useCsView({
  // highlight-start
  budgetRange: useCsInputNumberRangeItem(
    "予算範囲",
    useRangeInit<number>(),
    numberRule(false, 1, 100000),
    RW.Editable,
    "最低予算価格を入力してください",
    "最高予算価格を入力してください"
  ),
  // highlight-end
});
```
