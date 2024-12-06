---
sidebar_position: 1
title: useCsRqAdvancedMutateLoadEvent
---

`useCsRqAdvancedMutateLoadEvent` は、API 呼び出し方式が Orval（拡張版）に対応する更新系 API ロードイベントを初期化するためのフックです。
複雑な検索条件などがあり POST でリクエストを渡して検索することを想定したロードイベントです。

## シグネチャ

<h3>
  <code>useCsRqAdvancedMutateLoadEvent<br/>&nbsp;&lt;TApiRequest, TApiResponse, TApiError, TContext = unknown><br/>(mutationResult: RqAdvancedMutationResult<br/>&nbsp;&lt;TApiResponse, TApiError, TApiRequest, TContext>,<br/>&nbsp;request: TApiRequest):<br/>CsRqAdvancedMutateLoadEvent<br/>&nbsp;&lt;TApiRequest, TApiResponse, TApiError, TContext></code>
</h3>

## 引数

| 引数名         | 必須 | 型                                                                           | 説明                                                               |
| -------------- | ---- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| mutationResult | 〇   | `RqAdvancedMutationResult<TApiResponse, TApiError, TApiRequest, TContext>*¹` | TanStack Query の `useMutate` を使ったカスタムフックを指定します。 |
| request        | 〇   | `TApiRequest`                                                                | API リクエストのパラメータを指定します。                           |

\*1：`RqAdvancedMutationResult`は API のリクエスト、レスポンス、エラー、コンテキストに関する情報を保持する型定義です。

## 返り値

API のレスポンス、成功・失敗のステータスなどの情報が含まれる`CsRqAdvancedMutateLoadEvent`クラスのインスタンスを返します。

## 使用例

```tsx
export const useTodoComplexSearchView = (): TodoComplexSearchView => {
  const title = useCsInputTextItem("検索するタイトル", useInit(""), stringRule(false));
  const description = useCsTextAreaItem("検索する説明文", useInit(""), stringRule(false));

  return useCsView(
    {
      title: title,
      description: description,
      loadEvent: useCsRqAdvancedMutateLoadEvent(
        useComplexSearchTodo(), // useMutateを返すカスタムフック
        { title: title.value ?? "", description: description.value ?? "" }
       ), // ロードイベントにリクエストを設定
    }
  );
};
```
