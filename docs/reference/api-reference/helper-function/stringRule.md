---
sidebar_position: 1
title: stringRule
---

`stringRule` は、文字列入力項目のバリデーションルールを生成するための関数です。この関数では、必須項目かどうか、最小・最大文字数、カスタムルール名を指定できます。

## シグネチャ

<h3>`stringRule(required: boolean, min?: number, max?: number, customRuleName?: string): StringValidationRule`</h3>

## 引数

| 引数名         | 必須 | 型        | 説明                                             |
| -------------- | ---- | --------- | ------------------------------------------------ |
| required       | 〇   | `boolean` | 入力項目が必須項目かどうかを指定します。         |
| min            |      | `number`  | 入力文字列の最小文字数を指定します。             |
| max            |      | `number`  | 入力文字列の最大文字数を指定します。             |
| customRuleName |      | `string`  | カスタムバリデーションルールの名前を指定します。 |

## 返り値

`string`型のバリデーション定義情報（必須項目かどうか、最小・最大文字数、カスタムルール名など）を保持する`StringValidationRule` クラスのインスタンスを返します。

## 使用例

```tsx
const myCustomValidationRules = {
  全角文字: stringCustomValidationRule(
    createRegExpValidator(/^[^ -~｡-ﾟ]*$/),
    (label: string) => `${label}は全角文字で入力してください`,
  ),
}

// 省略

const view = useCsView(
  {
    title: useCsInputTextItem(
      "タイトル",
      useInit(""),
      // highlight-start
      stringRule(true, 1, 10, "全角文字")
      // highlight-end
    ),
  },
  {
    customValidationRules: myCustomValidationRules,
  }
);
```
