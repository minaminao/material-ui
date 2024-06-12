---
productId: base-ui
title: React Form Control component and hook
components: FormControl
hooks: useFormControlContext
githubLabel: 'component: FormControl'
---

# Form Control

<p class="description">The Form Control component is a utility that lets you associate a form input with auxiliary components, such as labels, error indicators, or helper text.</p>

{{"component": "@mui/docs/ComponentLinkHeader", "design": false}}

{{"component": "modules/components/ComponentPageTabs.js"}}

## Introduction

Form Control is a utility that wraps an input component with other associated components in order to make the state of the input available to those components.

フォームコントロールは、入力コンポーネントを他の関連コンポーネントでラップし、それらのコンポーネントで入力のステートを利用できるようにするユーティリティです。

For instance, you may want to show an additional element asking the user to enter a value if the input is empty, or display a warning icon if the entered value is incorrect.

例えば、入力が空の場合にユーザーに値の入力を求める追加要素を表示したり、入力された値が正しくない場合に警告アイコンを表示したりできます。

## Component

```jsx
import { FormControl } from '@mui/base/FormControl';
```

Form Control wraps around the elements of a form that need access to the state of an `<input>`.
For instance, if the form's **Submit** button needs to change states after the user enters information, then the component will be structured like this:

フォームコントロールは `<input>` のステートへのアクセスが必要なフォームの要素をラップします。
例えば、フォームの **Submit** ボタンがユーザが情報を入力した後にステートを変更する必要がある場合、コンポーネントはこのような構造になります:

```jsx
<FormControl>
  <input>
  <button>Submit</button>
</FormControl>
```

The following demo shows how to create and style a form that uses Form Control to wrap the elements of the form.
Note that it also uses the `useFormControlContext` hook in order to pass props to the custom Input—see the [Hook](#hook) section below for more details.

次のデモでは、フォームコントロールを使ってフォームの要素をラップするフォームの作成方法とスタイルを示しています。
また、カスタムInputにpropsを渡すために `useFormControlContext` フックを使用していることに注意してください。詳細は下記の [Hook](#hook) セクションを参照してください。

{{"demo": "BasicFormControl"}}

### Usage with TypeScript

In TypeScript, you can specify the custom component type used in the `slots.root` as a generic parameter of the unstyled component.
This way, you can safely provide the custom root's props directly on the component:

```tsx
<FormControl<typeof CustomComponent> slots={{ root: CustomComponent }} customProp />
```

The same applies for props specific to custom primitive elements:

```tsx
<FormControl<'button'> slots={{ root: 'button' }} onClick={() => {}} />
```

## Hook

```jsx
import { useFormControlContext } from '@mui/base/FormControl';
```

The `useFormControlContext` hook reads the context provided by Form Control.
This hook lets you work with custom input components inside of the Form Control.
You can also use it to read the form control's state and react to its changes in a custom component.

Hooks _do not_ support [slot props](#custom-structure), but they do support [customization props](#customization).

:::info
Hooks give you the most room for customization, but require more work to implement.
With hooks, you can take full control over how your component is rendered, and define all the custom props and CSS classes you need.

You may not need to use hooks unless you find that you're limited by the customization options of their component counterparts—for instance, if your component requires significantly different [structure](#anatomy).
:::

The demo below shows how to integrate this hook with its component counterpart:

- `CustomInput` is a wrapper around a native HTML `<input>` that adds Form Control integration.
- `ControlStateDisplay` reads the state of the form control and displays it as text.

{{"demo": "UseFormControl.js", "defaultCodeOpen": false}}

Note that even though Form Control supports both controlled and uncontrolled-style APIs (that is it accepts `value` and `defaultValue` props), `useFormControlContext` returns only the controlled `value`.
This way, you don't have to implement both in your custom input—Form Control does this for you.

:::info

- A component is **controlled** when it's managed by its parent using props.
- A component is **uncontrolled** when it's managed by its own local state.

Learn more about controlled and uncontrolled components in the [React documentation](https://react.dev/learn/sharing-state-between-components#controlled-and-uncontrolled-components).
:::

## Customization

:::info
The following features can be used with both components and hooks.
For the sake of simplicity, demos, and code snippets primarily feature components.
:::

### Accessing the form control state

You can access the state of the Form Control by providing a function as a child.
The state will be provided as a parameter to this function.

The following demo shows how to access the state of the Form Control in an Input component nested inside:

{{"demo": "FormControlFunctionChild.js"}}
