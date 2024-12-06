---
sidebar_position: 1
title: useCsMultiCheckBoxItem
---

`useCsMultiCheckBoxItem` は、複数選択可能なチェックボックスに対応する Item を初期化するためのフックです。

## シグネチャ

<h3>`useCsMultiCheckBoxItem(label, state, rule, selOpt?, readonly?): CsMultiCheckBoxItem`</h3>

## 引数

| 引数名   | 必須 | 型                            | 説明                                                                                                                                                              |
| -------- | ---- | ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label    | 〇   | `string`                      | 入力項目のラベルを指定します。                                                                                                                                    |
| state    | 〇   | `StateResult<string[]>*¹`     | 入力項目の状態変数を指定します。[useInit](../helper-function/useInit.md) を使用して初期化した状態変数を指定します。                                               |
| rule     | 〇   | `StringArrayValidationRule*²` | 入力項目のバリデーションルールを指定します。 [stringArrayRule](../helper-function/stringArrayRule.md)を使用して初期化したルールを指定します。                     |
| selOpt   |      | `SelectOptions`               | チェックボックスの選択肢を指定します。[selectOptions](../helper-function/selectOptions.md) を使用して初期値を指定します。                                                                                                                           |
| readonly |      | `RW.Editable \| RW.Readonly`  | 入力項目が読み取り専用かどうかを指定します。`RW.Editable` は読み取り・書き込み可能、`RW.Readonly`は読み取り専用を表す値です。デフォルトは `RW.Editable` です。 　 |

\*1：`StateResult`は `useState` の戻り値を管理する型定義です。詳しくは[useInit](../helper-function/useInit.md)を参照してください。

\*2：`StringArrayValidationRule`は`string[]`型のバリデーション定義情報（必須項目かどうか、カスタムルール名など）を保持する型定義です。

## 返り値

引数で定義した初期値やバリデーションルール、選択肢など、複数選択可能なチェックボックス項目に関する情報が集約された `CsMultiCheckBoxItem` クラスのインスタンスを返します。

## 使用例

```tsx
useCsView({
  // highlight-start
  interests: useCsMultiCheckBoxItem(
    "興味のある分野",
    useInit<string[]>([]),
    stringArrayRule(false),
    selectOptions(
      [
        { key: "technology", name: "テクノロジー" },
        { key: "music", name: "音楽" },
        { key: "sport", name: "スポーツ" },
        { key: "art", name: "アート" },
        { key: "movies", name: "映画" },
        { key: "reading", name: "読書" },
        { key: "travel", name: "旅行" },
        { key: "cooking", name: "料理" },
        { key: "gaming", name: "ゲーム" },
        { key: "fashion", name: "ファッション" },
        { key: "health", name: "健康" },
        { key: "education", name: "教育" },
      ],
      "key",
      "name"
    )
  ),
  // highlight-end
});
```
