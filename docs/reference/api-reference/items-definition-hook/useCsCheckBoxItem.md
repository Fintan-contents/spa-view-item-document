---
sidebar_position: 1
title: useCsCheckBoxItem
---

`useCsCheckBoxItem` は、チェックボックスに対応する Item を初期化するためのフックです。

## シグネチャ

<h3>`useCsCheckBoxItem(label, state, checkBoxText, readonly?): CsCheckBoxItem`</h3>

## 引数

| 引数名       | 必須 | 型                           | 説明                                                                                                                                                              |
| ------------ | ---- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label        | 〇   | `string`                     | 入力項目のラベルを指定します。                                                                                                                                    |
| state        | 〇   | `StateResult<boolean>*¹`     | 入力項目の状態変数を指定します。[useInit](../helper-function/useInit.md) を使用して初期化した状態変数を指定します。                                               |
| checkBoxText | 〇   | `string`                     | チェックボックスのテキストを指定します。                                                                                                                          |
| readonly     |      | `RW.Editable \| RW.Readonly` | 入力項目が読み取り専用かどうかを指定します。`RW.Editable` は読み取り・書き込み可能、`RW.Readonly`は読み取り専用を表す値です。デフォルトは `RW.Editable` です。 　 |

\*1：`StateResult`は `useState` の戻り値を管理する型定義です。詳しくは[useInit](../helper-function/useInit.md)を参照してください。

## 返り値

引数で定義した初期値やチェックボックスのテキストなど、チェックボックス入力項目に関する情報が集約された `CsCheckBoxItem` クラスのインスタンスを返します。

## 使用例

```tsx
useCsView({
  // highlight-start
  newsOk: useCsCheckBoxItem("お知らせを受け取る", useInit(), "受け取る"),
  // highlight-end
});
```
