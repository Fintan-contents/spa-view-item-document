---
sidebar_position: 1
title: useCsInputTextItem
---

`useCsInputTextItem` は、テキスト入力ボックスに対応する Item を初期化するためのフックです。

## シグネチャ

<h3>`useCsInputTextItem(label, state, rule, readonly?, placeholder?): CsInputTextItem`</h3>

## 引数

| 引数名      | 必須 | 型                           | 説明                                                                                                                                                           |
| ----------- | ---- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label       | 〇   | `string`                     | 入力項目のラベルを指定します。 　                                                                                                                              |
| state       | 〇   | `StateResult<string>*¹`      | 入力項目の状態変数を指定します。[useInit](../helper-function/useInit.md) を使用して初期化した状態変数を指定します。                                            |
| rule        | 〇   | `StringValidationRule*²`     | 入力項目のバリデーションルールを指定します。[stringRule](../helper-function/stringRule.md)を使用して初期化したルールを指定します。                             |
| readonly    |      | `RW.Editable \| RW.Readonly` | 入力項目が読み取り専用かどうかを指定します。`RW.Editable` は読み取り・書き込み可能、`RW.Readonly`は読み取り専用を表す値です。デフォルトは `RW.Editable` です。 |
| placeholder |      | `string`                     | プレースホルダーを指定します。                                                                                                                                 |

\*1：`StateResult`は `useState` の戻り値を管理する型定義です。詳しくは[useInit](../helper-function/useInit.md)を参照してください。

\*2：`StringValidationRule`は`string`型のバリデーション定義情報（必須項目かどうか、最小・最大文字数、カスタムルール名など）を保持する型定義です。

## 返り値

引数で定義した初期値やバリデーションルールなど、入力項目に関する情報が集約された `CsInputTextItem` クラスのインスタンスを返します。

## 使用例

```tsx
useCsView({
  // highlight-start
  inputTextItem: useCsInputTextItem(
    "名前",
    useInit(""),
    stringRule(true, 1, 10),
    RW.Editable,
    "入力してください"
  ),
  // highlight-end
});
```