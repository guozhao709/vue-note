# Props

## 概念

props 是一个工具, 用来进行父子组件间的数据通信

## 响应式 props 解构(vue3.5+)

在 vue3.5+中, props 进行解构时, 会在属性名上前加上 props.

```js
const props = defineProps({
    name: String,
    age: Number,
});
// 一般通过 props.name 或 props.age 访问, 若 name 或 age 为一个ref, 则会保留响应式
// 在使用watch时, 由于是props.xxx, 所以要用函数的形式返回

// 在3.5版本之前
const { name, age } = defineProps({
    name: String,
    age: Number,
});
// 这样做会失去响应式
// 3.5版本之后, 解构时会自动保留响应式
```

## 使用一个对象绑定多个 props

```js
const obj = {
    name: '张三',
    age: 20,
    sex: '男'
}

<ObjTest v-bind="post" />
// 等价于
<ObjTest :name="post.name" :age="post.age" :sex="post.sex" />
```

## 单向数据流

props 是单向数据流, 父组件向子组件传递数据, 子组件不能修改父组件的 props 数据。

## props 校验

```js
defineProps({
    // 基础类型检查
    // (给出 `null` 和 `undefined` 值则会跳过任何类型检查)
    propA: Number,
    // 多种可能的类型
    propB: [String, Number],
    // 必传，且为 String 类型
    propC: {
        type: String,
        required: true,
    },
    // 必传但可为 null 的字符串
    propD: {
        type: [String, null],
        required: true,
    },
    // Number 类型的默认值
    propE: {
        type: Number,
        default: 100,
    },
    // 对象类型的默认值
    propF: {
        type: Object,
        // 对象或数组的默认值
        // 必须从一个工厂函数返回。
        // 该函数接收组件所接收到的原始 prop 作为参数。
        default(rawProps) {
            return { message: "hello" };
        },
    },
    // 自定义类型校验函数
    // 在 3.4+ 中完整的 props 作为第二个参数传入
    propG: {
        validator(value, props) {
            // The value must match one of these strings
            return ["success", "warning", "danger"].includes(value);
        },
    },
    // 函数类型的默认值
    propH: {
        type: Function,
        // 不像对象或数组的默认，这不是一个
        // 工厂函数。这会是一个用来作为默认值的函数
        default() {
            return "Default function";
        },
    },
});
```
