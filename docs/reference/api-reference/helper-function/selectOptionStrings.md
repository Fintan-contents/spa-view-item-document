---
sidebar_position: 1
title: selectOptionStrings
---

`selectOptionStrings` は、文字列の配列をセレクトボックスやマルチチェックボックスなどの選択肢に変換するための関数です。

## シグネチャ

<h3>`selectOptionStrings(options: string[]): SelectOptions`</h3>

## 引数

| 引数名 | 必須 | 型        | 説明                                                                                   |
| ------ | ---- | --------- | -------------------------------------------------------------------------------------- |
| options| 〇   | `string[]` | セレクトボックスの選択肢となる文字列の配列を指定します。                                |

## 返り値

選択肢の配列とキー情報を保持した `SelectOptions` クラスのインスタンスを返します。

## 使用例

```tsx
const colors = ["赤", "青", "緑"];

useCsView({
  favoriteColor: useCsSelectBoxItem(
    "好きな色",
    useInit(),
    stringRule(true),
    selectOptionStrings(colors),
    RW.Editable,
    "好きな色を選択してください"
  ),
});