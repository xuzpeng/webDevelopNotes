h5编码规范table里面为tbody，tbody里面必须放 tr。

子组件的数据必须为函数，即data为函数，return 数据。

> 使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 `v-on:click.prevent.self`  会阻止**所有的点击**，而 `v-on:click.self.prevent ` 只会阻止对元素自身的点击。

```vue
<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>
```

不像其它只能对原生的 DOM 事件起作用的修饰符，`.once` 修饰符还能被用到自定义的组件事件上。

> 请注意修饰键与常规按键不同，在和 `keyup` 事件一起用时，事件触发时修饰键必须处于按下状态。换句话说，只有在按住 `ctrl` 的情况下释放其它按键，才能触发 `keyup.ctrl`。而单单释放 `ctrl` 也不会触发事件。如果你想要这样的行为，请为 `ctrl` 换用 `keyCode`：`keyup.17`。

`.exact` 修饰符允许你控制由精确的系统修饰符组合触发的事件。

# 单向数据流

父组件向子组件传值，子组件不允许改变父组件的值。

# props 特性与非 props 特性

props特性：父组件传值，子组件接收，不会显示在DOM标签中。

非 props 特性：父组件传值，子组件不接收，会显示在DOM标签中。

# 解析 DOM 模板时的注意事项

有些 HTML 元素，诸如 `<ul>`、`<ol>`、`<table>` 和 `<select>`，对于哪些元素可以出现在其内部是有严格限制的。而有些元素，诸如 `<li>`、`<tr>` 和 `<option>`，只能出现在其它某些特定的元素内部。

这会导致我们使用这些有约束条件的元素时遇到一些问题。例如： 

```vue
<table>
  <blog-post-row></blog-post-row>
</table>
```

这个自定义组件 `<blog-post-row>` 会被作为无效的内容提升到外部，并导致最终渲染结果出错。幸好这个特殊的 `is` 特性给了我们一个变通的办法：

```vue
<table>
  <tr is="blog-post-row"></tr>
</table>
```



需要注意的是**如果我们从以下来源使用模板的话，这条限制是不存在的**：

- 字符串 (例如：`template: '...'`)
- 单文件组件 (.vue)
- &lt;script type="text/x-template"&gt;

