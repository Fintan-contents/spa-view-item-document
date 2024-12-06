---
sidebar_position: 1
title: useCsInputDateRangeItem
---

`useCsInputDateRangeItem` は、日付範囲入力ボックスに対応する Item を初期化するためのフックです。

## シグネチャ

<h3>`useCsInputDateRangeItem(label, state, rule, readonly?, lowerPlaceholder?, upperPlaceholder?): CsInputDateRangeItem`</h3>

## 引数

| 引数名           | 必須 | 型                           | 説明                                                                                                                                                              |
| ---------------- | ---- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label            | 〇   | `string`                     | 入力項目のラベルを指定します。                                                                                                                                    |
| state            | 〇   | `StateResult<string[]>*¹`    | 入力項目の状態変数を指定します。[useRangeInit](../helper-function/useRangeInit.md) を使用して初期化した状態変数を指定します。                                     |
| rule             | 〇   | `StringArrayValidationRule*²`| 入力項目のバリデーションルールを指定します。[stringArrayRule](../helper-function/stringArrayRule.md)を使用して初期化したルールを指定します。                      |
| readonly         |      | `RW.Editable \| RW.Readonly` | 入力項目が読み取り専用かどうかを指定します。`RW.Editable` は読み取り・書き込み可能、`RW.Readonly`は読み取り専用を表す値です。デフォルトは `RW.Editable` です。 　 |
| lowerPlaceholder |      | `string`                     | 下限日付のプレースホルダーを指定します。                                                                                                                          |
| upperPlaceholder |      | `string`                     | 上限日付のプレースホルダーを指定します。                                                                                                                          |

\*1：`StateResult`は `useState` の戻り値を管理する型定義です。詳しくは[useRangeInit](../helper-function/useRangeInit.md)を参照してください。

\*2：`StringArrayValidationRule`は`string[]`型のバリデーション定義情報（必須項目かどうか、カスタムルール名など）を保持する型定義です。

## 返り値

引数で定義した初期値やバリデーションルールなど、日付範囲入力項目に関する情報が集約された `CsInputDateRangeItem` クラスのインスタンスを返します。

## 使用例

```tsx
useCsView({
  // highlight-start
  subscriptionPeriod: useCsInputDateRangeItem(
    "購読期間",
    useRangeInit("2020-01-01", "2020-12-31"),
    stringArrayRule(true),
    RW.Editable,
    "開始日を入力してください",
    "終了日を入力してください"
  ),
  // highlight-end
});
```
