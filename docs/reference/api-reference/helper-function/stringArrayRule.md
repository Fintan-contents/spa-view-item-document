---
sidebar_position: 1
title: stringArrayRule
---

`stringArrayRule` は、文字列配列入力項目のバリデーションルールを生成するための関数です。この関数では、必須項目かどうか、カスタムルール名を指定できます。

## シグネチャ

<h3>`stringArrayRule(required: boolean, customRuleName?: string): StringArrayValidationRule`</h3>

## 引数

| 引数名         | 必須 | 型        | 説明                                             |
| -------------- | ---- | --------- | ------------------------------------------------ |
| required       | 〇   | `boolean` | 入力項目が必須項目かどうかを指定します。         |
| customRuleName |      | `string`  | カスタムバリデーションルールの名前を指定します。 |

## 返り値

`string[]` 型のバリデーション定義情報（必須項目かどうか、カスタムルール名など）を保持する `StringArrayValidationRule` クラスのインスタンスを返します。

## 使用例

```tsx
const view = useCsView(
  {
    interests: useCsMultiCheckBoxItem(
      "興味のある分野",
      useInit<string[]>([]),
      stringArrayRule(false, "興味ある分野の最大要素数"),
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
  },
  {
    customValidationRules: myCustomValidationRules, // 「興味ある分野の最大要素数」のカスタムバリデーションルールを定義済み
  }
);
```
