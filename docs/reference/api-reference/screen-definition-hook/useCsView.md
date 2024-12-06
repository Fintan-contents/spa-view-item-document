---
sidebar_position: 2
title: useCsView
---

`useCsView` は、画面項目を 1 つの View（画面）として初期化するためのフックです。カスタムバリデーションルールの定義オブジェクトやバリデーションの実行タイミングなど、追加のオプションを指定できます。

## シグネチャ

<h3>`useCsView(definitions, options?, validationEventHook?): CsView & D`</h3>

## 引数

<table>
  <thead>
    <tr>
      <th>引数名</th>
      <th>必須</th>
      <th>型</th>
      <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>definitions</td>
      <td>〇</td>
      <td><code>D extends CsViewDefinition*¹</code></td>
      <td>開発者が定義した画面項目の型を指定します。画面項目には<a href="../../../category/入力項目定義のフック">入力項目定義のフック</a>や<a href="../../../category/イベント定義のフック">イベント定義のフック</a>を指定できます。</td>
    </tr>
    <tr>
      <td>options</td>
      <td></td>
      <td><code> readonly?: boolean, customValidationRules?: AppValidationRules extends CustomValidationRules,*² validationTrigger?: "onSubmit" | "onBlur"</code></td>
      <td><p><code>readonly</code>には読み取り専用にするかどうかを指定します。 デフォルトは<code>false</code>です。</p>
        <p><code>customValidationRules</code>には適用したいカスタムバリデーションルールの定義オブジェクトを指定します。詳細は<a href="../../../implementation-guide/tips/add-custom-validation">カスタムバリデーションの追加方法</a>を参照してください。</p>
        <code>validationTrigger</code>にはバリデーションの実行タイミングを指定します。<code>onSubmit</code>はボタン押下時、<code>onBlur</code>は入力項目からフォーカスが外れたタイミングでバリデーションを実行します。デフォルトは<code>onSubmit</code>です。</td>
    </tr>
    <tr>
      <td>validationEventHook</td>
      <td></td>
      <td><code>(instance: CsView & D, customValidationRules?: CustomValidationRules\*²) => CsValidationEvent\*³</code></td>
      <td>利用者は直接指定することは通常ありません。<p/>
      導入ツールでインストールした際にYupかZodのイベントが指定されるようになっています。</td>
    </tr>
  </tbody>
</table>

\*1: `CsViewDefinition`は、キーが`string`、値が`CsItemBase`または`CsEvent`のみを許容する`Record`型です。

\*2: `CustomValidationRules`は、キーがルール名で、値が[CustomValidationRule](../../../category/カスタムバリデーション定義の関数)のオブジェクトです。

\*3: `CsValidationEvent`はバリデーション処理を行うイベントです。Yup の実装クラスと Zod の実装クラスがあります。

## 返り値

画面項目が 1 つに集約された`CsView`の拡張クラスのインスタンスを返します。
返り値の正確な型は `CsView & D` で、`D` は、定義した画面項目とイベントのオブジェクトの型になります。

## 使用例

```tsx
const view = useCsView(
  {
    title: useCsInputTextItem("タイトル", useInit(""), stringRule(true, 1, 10)),
    description: useCsTextAreaItem(
      "説明",
      useInit(""),
      stringRule(true, 1, 100)
    ),
    createButton: useCsRqMutateButtonClickEvent(usePostTodo()),
  },
  {
    readonly: true,
    customValidationRules: {
      ...buildInCustomValidationRules, // 組み込みのルールオブジェクトを指定
      ...myCustomValidationRules, // 独自のルールオブジェクトを指定
    }
    validationTrigger: "onBlur",
  }
);
```
