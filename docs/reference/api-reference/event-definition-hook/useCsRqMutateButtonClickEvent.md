---
sidebar_position: 1
title: useCsRqMutateButtonClickEvent
---

`useCsRqMutateButtonClickEvent` は、API 呼び出し方式が TanStack Query および Orval（シンプル版）に対応する更新系 API ボタンイベントを初期化するためのフックです。

## シグネチャ

<h3>
  <code>useCsRqMutateButtonClickEvent<br/>&nbsp;&lt;TApiRequest, TApiResponse, TApiError, TContext = unknown><br/>(mutationResult: UseMutationResult<br/>&nbsp;&lt;TApiResponse, TApiError, TApiRequest, TContext>):<br/>CsMutateButtonClickEvent<br/>&nbsp;&lt;TApiRequest, TApiResponse, TApiError, TContext></code>
</h3>

## 引数

| 引数名         | 必須 | 型                                                                           | 説明                                                               |
| -------------- | ---- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| mutationResult | 〇   | `UseMutationResult<TApiResponse, TApiError, TApiRequest, TContext>*¹` | TanStack Query の `useMutate` を使ったカスタムフックを指定します。 |

\*1：`UseMutationResult`は API のリクエスト、レスポンス、エラー、コンテキストに関する情報を保持するTanStack Queryの組み込みの型定義です。

## 返り値

API のリクエストやレスポンス、成功・失敗のステータスなどの情報が含まれる`CsMutateButtonClickEvent`クラスのインスタンスを返します。

## 使用例

```tsx
export const useTodoPostView = (): TodoPostView => {
  return useCsView(
    {
      title: useCsInputTextItem(
        "タイトル",
        useInit(""),
        stringRule(false, 1, 10)
      ),
      description: useCsTextAreaItem("説明", useInit(""), stringRule(false)),
      // highlight-start
      createButton: useCsRqMutateButtonClickEvent(usePostTodo()),
      // highlight-end
    },
    {
      validationTrigger: "onBlur", // カーソルが離れたタイミングでバリデーションを実行
    }
  );
};
```