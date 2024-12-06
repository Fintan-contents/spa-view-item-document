---
sidebar_position: 1
title: 入力部品一覧
---

省力化コンポーネントが提供する各種入力部品について、部品用途、画面コンポーネント、Item、フックの対応表を以下に示します。

### テキスト入力部品

| 部品用途           | 画面コンポーネント | Item                  | フック                   |
| ------------------ | ------------------ | --------------------- | ------------------------ |
| テキスト入力       | `AxInputText`      | `CsInputTextItem`     | `useCsInputTextItem`     |
| パスワード入力     | `AxInputPassword`  | `CsInputPasswordItem` | `useCsInputPasswordItem` |
| 複数行テキスト入力 | `AxTextArea`       | `CsTextAreaItem`      | `useCsTextAreaItem`      |

### 数値入力部品

| 部品用途     | 画面コンポーネント   | Item                     | フック                      |
| ------------ | -------------------- | ------------------------ | --------------------------- |
| 数値入力     | `AxInputNumber`      | `CsInputNumberItem`      | `useCsInputNumberItem`      |
| 数値範囲入力 | `AxInputNumberRange` | `CsInputNumberRangeItem` | `useCsInputNumberRangeItem` |

### 日付入力部品

| 部品用途     | 画面コンポーネント | Item                   | フック                    |
| ------------ | ------------------ | ---------------------- | ------------------------- |
| 日付入力     | `AxInputDate`      | `CsInputDateItem`      | `useCsInputDateItem`      |
| 日付範囲入力 | `AxInputDateRange` | `CsInputDateRangeItem` | `useCsInputDateRangeItem` |

### 選択部品

| 部品用途             | 画面コンポーネント  | Item                    | フック                     |
| -------------------- | ------------------- | ----------------------- | -------------------------- |
| ラジオボックス       | `AxRadioBox`        | `CsRadioBoxItem`        | `useCsRadioBoxItem`        |
| チェックボックス     | `AxCheckBox`        | `CsCheckBoxItem`        | `useCsCheckBoxItem`        |
| 複数チェックボックス | `AxMultiCheckBox`   | `CsMultiCheckBoxItem`   | `useCsMultiCheckBoxItem`   |
| セレクトボックス     | `AxSelectBox`       | `CsSelectBoxItem`       | `useCsSelectBoxItem`       |
| 数値セレクトボックス | `AxSelectNumberBox` | `CsSelectNumberBoxItem` | `useCsSelectNumberBoxItem` |
