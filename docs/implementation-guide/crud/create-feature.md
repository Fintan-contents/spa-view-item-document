---
sidebar_position: 3
title: 登録機能
---

本節では以下に示すような登録機能の実装方法について説明します。

![登録機能の画面](../../../static/img/crud-create.gif)

## イベントの型を定義する

登録機能のイベントの型定義には`CsMutateButtonClickEvent`を指定します。登録用の View（`TodoCreateView`）のプロパティにイベントの型を定義します。型パラメータには 登録 API のリクエスト、レスポンスの型を指定します。

```ts title="src/app/todo/page.view.ts"
// Orvalで自動生成されたTodoRegistrationの型定義をimport

/**
 * 登録用のViewの型定義
 */
export type TodoCreateView = CsView & {
  title: CsInputTextItem;
  description: CsTextAreaItem;
  assignee: CsInputTextItem;
  // highlight-start
  createButton: CsMutateButtonClickEvent<
    // APIのリクエストデータ型を定義
    {
      data: TodoRegistration; // TodoRegistration型を定義
    },
    Todo // APIのレスポンスデータ型を定義
  >;
  // highlight-end
};
```

## イベントを初期化する

登録用の View（`TodoCreateView`）にイベントの初期化処理を追加します。登録 API では Event のフックに`useCsRqAdvancedMutateButtonClickEvent()`、引数には Orval で自動生成された API フック`usePostTodo()`を指定します。

```ts title="src/app/todo/page.view.ts"
// Orvalで自動生成されたAPIフック（usePostTodo）をimport

/**
 * 登録用のViewの初期化
 *
 * @returns TodoPostView 登録用のView
 */
export const useTodoCreateView = (): TodoCreateView => {
  return useCsView({
    title: useCsInputTextItem("タイトル", useInit(""), stringRule(true, 1, 20), RW.Editable, "タイトルを入力してください"),
    description: useCsTextAreaItem("説明", useInit(""), stringRule(true, 1, 100), RW.Editable, "タスクの説明を入力してください"),
    assignee: useCsInputTextItem("担当者", useInit(""), stringRule(true, 1, 20), RW.Editable, "担当者を入力してください"),
    // highlight-start
    createButton: useCsRqAdvancedMutateButtonClickEvent(usePostTodo()), // イベントの初期化処理の追加
    // highlight-end
  });
};
```

### View の定義を呼び出す

[イベントを初期化する](./create-feature.md#イベントを初期化する)で定義した 登録用の View 定義を呼び出します。

```tsx title="src/app/todo/TodoCreateModal.tsx"
const todoCreateView = useTodoCreateView(); // 登録用のViewの呼び出し
```

## ボタンを配置する

登録ボタンを配置する際は、画面コンポーネントとして `AxMutateButton` を使用します。（型定義で用いた `CsMutateButtonClickEvent` に対応した画面コンポーネントを使用します。）

`event` という Props に、対応するイベントの変数を指定します。また、`validationViews`に View の変数を指定することで、バリデーションが実行できます。

```tsx title="src/app/todo/TodoCreateModal.tsx"
<Modal
  open={isOpenCreateModal}
  title="追加"
  onCancel={onCancel}
  footer={
    // highlight-start
    <AxMutateButton event={todoCreateView.createButton} validationViews={[todoCreateView]} type="primary" onAfterApiCallSuccess={onAfterApiCallSuccess}>
      作成
    </AxMutateButton>
    // highlight-end
  }
>
  <>
    <AxInputText item={todoCreateView.title}></AxInputText>
    <AxTextArea item={todoCreateView.description}></AxTextArea>
    <AxInputText item={todoCreateView.assignee}></AxInputText>
  </>
</Modal>
```

## 登録 API に必要なリクエストを設定する

登録 API 呼び出し時に指定する API リクエストを指定します。`data`に登録するデータを指定します。

```tsx title="src/app/todo/TodoCreateModal.tsx"
const todoCreateView = useTodoCreateView(); // 登録用のViewの呼び出し

// highlight-start
todoCreateView.createButton.setRequest({
  // リクエストデータに値をセット
  data: {
    title: todoCreateView.title.value ?? "",
    description: todoCreateView.description.value ?? "",
    assignee: todoCreateView.assignee.value ?? "",
  },
});
// highlight-end
```

以上で、登録機能の実装が完了します。ボタン押下時に登録 API が呼び出されているか確認してください。
