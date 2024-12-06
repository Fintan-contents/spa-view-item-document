---
sidebar_position: 3
title: 特徴
---

# 特徴

[前節](./basic-concepts.md)で述べた 3 つのコンセプトに基づいて実装されている省力化コンポーネントは、次のような特徴を持ちます。

- <strong>入力項目の定義が 1-2 行で書ける</strong>
- <strong>バリデーションの定義が簡潔に書ける</strong>
- <strong>高機能なボタンが使える</strong>
- <strong>自動レイアウト機能が使える</strong>

## 入力項目の定義が 1-2 行で書ける

省力化コンポーネントを使用することで、入力項目の定義を 1-2 行で書くことができます。

以下の画面を例に考えてみます。

![入力項目の定義2個](/img/screen-item-2.png)

画面には 2 種類の入力項目があります。省力化コンポーネントを用いることで、これらの入力項目をそれぞれ 1-2 行で定義できます。

```tsx
// ＝＝＝＝＝＝＝＝
// 入力項目の定義
// ＝＝＝＝＝＝＝＝
// View 定義
export type RegisterUserView = CsView & {
  userName: CsInputTextItem;
  password: CsInputPasswordItem;
};

export const RegisterUserComponent: React.FC = () => {
  // Viewの作成
  const view: RegisterUserView = useCsView({
    userName: useCsInputTextItem(
      "ユーザー名",
      useInit(""),
      stringRule(true, 3, 30),
    ),
    password: useCsInputPasswordItem(
      "パスワード",
      useInit(""),
      stringRule(true, 8, 16),
    ),
  });

  // ＝＝＝＝＝＝＝＝
  // 入力項目の配置
  // ＝＝＝＝＝＝＝＝
  return (
    <>
      <AxInputText item={view.userName} />
      <AxInputPassword item={view.password} />
    </>
  );
};
```

このように入力項目を Item で定義し、コンポーネントに Item 情報を渡すことで、ラベル、バリデーションメッセージ表示領域、イベントハンドラなどを持った高機能な入力項目を配置できます。

仮に入力項目を増やしたい場合でも、1 項目につき 1-2 行コードを増やすだけで実装可能です。

```tsx
// View 定義
export type RegisterUserView = CsView & {
  userName: CsInputTextItem;
  password: CsInputPasswordItem;
  mailAddress: CsInputTextItem;
  age: CsInputNumberItem;
  gender: CsRadioBoxItem;
  birthDay: CsInputDateItem;
};

export const RegisterUserComponent: React.FC = () => {
  // Viewの作成
  const view: RegisterUserView = useCsView({
    userName: useCsInputTextItem(
      "ユーザー名",
      useInit(""),
      stringRule(true, 3, 30),
    ),
    password: useCsInputPasswordItem(
      "パスワード",
      useInit(""),
      stringRule(true, 8, 16),
    ),
    // 以下の4項目を追加
    mailAddress: useCsInputTextItem(
      "メールアドレス",
      useInit(""),
      stringRule(true, 8, 20),
    ),
    age: useCsInputNumberItem("年齢", useInit(), numberRule(true, 0)),
    gender: useCsRadioBoxItem(
      "性別",
      useInit(""),
      stringRule(true),
      selectOptionStrings(["男性", "女性", "回答しない"]),
    ),
    birthDay: useCsInputDateItem(
      "生年月日",
      useInit("2000-01-01"),
      stringRule(true),
    ),
  });

  return (
    <>
      <AxInputText item={view.userName} />
      <AxInputPassword item={view.password} />
      {/* 以下の4項目を追加 */}
      <AxInputText item={view.mailAddress} />
      <AxInputNumber item={view.age} />
      <AxRadioBox item={view.gender} />
      <AxInputDate item={view.birthDay} />
    </>
  );
};
```

6 項目になった画面は以下の通りです。

![入力項目の定義6個](/img/screen-item-6.png)

入力項目を簡潔に書けることで、項目が増えた場合でもコードが冗長にならず、保守性が向上します。

より詳しい実装方法については[実装ガイド](../category/実装ガイド)を参照してください。

## バリデーションの定義が簡潔に書ける

省力化コンポーネントを使用することでバリデーションの定義が簡潔に書けます。そのため、開発者は複雑なバリデーションロジックを手動で記述する必要がなくなり、View 定義にのみ集中できます。

Item 定義の第 3 引数に実施したいバリデーションルールを定義します。

```tsx
// View 定義
export type RegisterUserView = CsView & {
  userName: CsInputTextItem;
  age: CsInputNumberItem;
};

export const RegisterUserComponent: React.FC = () => {
  // Viewの作成
  const view: RegisterUserView = useCsView({
    // stringRuleでバリデーションを定義
    userName: useCsInputTextItem(
      "ユーザー名",
      useInit(""),
      stringRule(true, 3, 30),
    ),
    // numberRuleでバリデーションを定義
    age: useCsInputNumberItem("年齢", useInit(), numberRule(true, 0)),
  });

  return (
    <>
      <AxInputText item={view.userName} />
      <AxInputNumber item={view.age} />
    </>
  );
};
```

例えば、`userName` という入力項目に対しては以下のようなバリデーションを定義しています。

`stringRule(true, 3, 30)`

このバリデーションの内容は以下の通りです。

- 文字列型
- 必須
- 最小文字数 3 文字
- 最大文字数 30 文字

このように、標準的なバリデーションルールを簡潔に指定できるため、入力項目のバリデーションの定義が効率的に行えます。また、文字列型以外にも、数値型のバリデーションを定義する `numberRule` や、配列型のバリデーションを定義する `stringArrayRule` を使用できます。さらに、カスタムバリデーションルールを用いると「半角数字」や「全角文字」など、より詳細なバリデーションも定義可能です。

これにより、アプリケーション固有の要件に合わせた柔軟なバリデーションが実現できます。

```tsx
// View 定義
export type RegisterUserView = CsView & {
  userName: CsInputTextItem;
  age: CsInputNumberItem;
};

export const RegisterUserComponent: React.FC = () => {
  // Viewの作成
  const view: RegisterUserView = useCsView(
    {
      // stringRuleの第4引数にカスタムバリデーションルール名を指定
      userName: useCsInputTextItem(
        "ユーザー名",
        useInit(""),
        stringRule(true, 3, 30, "全角文字"),
      ),
      age: useCsInputNumberItem("年齢", useInit(), numberRule(true, 0)),
    },
    {
      customValidationRules: globalCustomValidationRules, // バリデーションルールの定義
    },
  );
  return (
    <>
      <AxInputText item={view.userName} />
      <AxInputNumber item={view.age} />
    </>
  );
};
```

この例のように、`stringRule` や他のルール関数の省略可能な 4 番目の引数としてカスタムバリデーションルールの名前を指定します。

より詳しい実装方法については[バリデーションを定義する](../implementation-guide/create-register-screen/define-validation.md)を参照してください。

## 高機能なボタンが使える

高機能なボタンは、アプリケーションのユーザビリティと開発効率を大幅に向上させる重要なコンポーネントです。

ボタンが持つ機能は以下の通りです。
いずれの機能も、従来は実装者がボタンの外部やハンドラ内に記述していたものです。省力化コンポーネントが提供するボタンでは、これらの機能が内部に組み込まれているため、実装者はパラメータを渡すだけで機能を実現できます。

- API 呼び出しの簡略化  
  CRUD（Create, Read, Update, Delete）機能に対応した API 呼び出しがシンプルに実装できます。イベントというクラスに API のフックをパラメータとして渡し、そのイベントをボタンに渡すことで動作します。

- バリデーションの実行  
  ボタンをクリックする前に必要なバリデーションを自動的に実行できるため、ユーザーからの入力データの整合性を確保できます。バリデーションを定義した View をボタンに渡すことで動作します。

- メッセージの表示機能  
  ボタン押下後に、メッセージやエラーメッセージを通知することが必要な場合は、メッセージ表示機能を使います。API 呼び出しの結果やバリデーションエラーなどの情報をユーザーに伝えられます。

- スピナー（Spinner）の表示  
  API 呼び出し中や処理が行われている間に視覚的なフィードバックをユーザーに提供します。これにより、不必要な再操作を防げます。ボタンに標準で組み込まれているため、追加で実装をせずに使用できます。

```tsx
// Viewの定義
export type TodosPostView = CsView & {
  title: CsInputTextItem;
  description: CsInputTextItem;
  createButton: CsMutateButtonClickEvent; // イベントの定義
};

// View の初期化
export const usePostTodoView = (): TodosPostView => {
  return useCsView({
    title: useCsInputTextItem(
      "タイトル",
      useInit(""),
      stringRule(true, 1, 100),
      RW.Editable,
      "タイトル",
    ),
    description: useCsInputTextItem(
      "説明",
      useInit(""),
      stringRule(true, 1, 100),
      RW.Editable,
      "説明",
    ),
    // ボタンイベントにAPI（usePostTodo）を渡す
    createButton: useCsRqMutateButtonClickEvent(usePostTodo()),
  });
};
```

上記のコードの `usePostTodo` は[TanStack Query](../prerequisite-knowledge.md#tanstack-query-公式サイト-tanstackquery) または [Orval](../prerequisite-knowledge.md#orval-公式サイト-orval) で自動生成されるコードです。

```tsx
export const PostTodoComponent = () => {
  const view = usePostTodoView();
  // 中略

  // APIのリクエストを設定
  view.createButton.setRequest({
    data: {
      title: view.title.value ?? "",
      description: view.description.value ?? "",
    },
  });

  return (
    <>
      {/* 中略 */}

      <AxMutateButton
        event={view.createButton} // 上記のViewで定義したcreateButtonイベントを渡す
        validationViews={[view]} // バリデーションしたいViewを渡す
        successMessage="Todoを追加しました"
        errorMessage="Todoの追加に失敗しました"
      >
        追加
      </AxMutateButton>
    </>
  );
};
```

より詳しい実装方法については[実装ガイド](../category/実装ガイド)を参照してください。

## 自動レイアウト機能が使える

省力化コンポーネントは入力項目の自動レイアウトに対応しています。以下に示す画面は、入力項目を横に 2 列ずつ並べた時の画面です。

![自動レイアウト](/img/automatic-layout.png)

次のコードは自動レイアウトの使用例です。

```tsx
<AxTableLayout view={view} colSize={2} />
```

- `view` にレイアウトに並べたい入力項目を含む View 定義を指定します。
- `colSize` に数値型を指定することで、指定した数値列ごとに入力項目を並べられます。

入力項目の並びが単純で機械的なレイアウトでよい場合は自動レイアウト機能が利用できます。入力項目の並びが複雑な場合やデザインを重視する場合は手動でレイアウトします。

より詳しい実装方法については[入力項目を配置する](../implementation-guide/create-register-screen/arrange-items.md)を参照してください。
