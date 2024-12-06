---
sidebar_position: 1
title: selectOptionNumbers
---

`selectOptionNumbers` は、数値の配列をセレクトボックスやマルチチェックボックスなどの選択肢に変換するための関数です。

## シグネチャ

<h3>`selectOptionNumbers(options: number[]): SelectOptions`</h3>

## 引数

| 引数名 | 必須 | 型        | 説明                                                                                   |
| ------ | ---- | --------- | -------------------------------------------------------------------------------------- |
| options| 〇   | `number[]` | セレクトボックスの選択肢となる数値の配列を指定します。                                |

## 返り値

選択肢の配列とキー情報を保持した `SelectOptions` クラスのインスタンスを返します。

## 使用例

```tsx
const columnSizes = [1, 2, 3, 4, 6];

useCsView({
  columnSize: useCsSelectBoxItem(
    "列数",
    useInit(),
    numberRule(true),
    selectOptionNumbers(columnSizes),
    RW.Editable,
    "列数を選択してください"
  ),
});