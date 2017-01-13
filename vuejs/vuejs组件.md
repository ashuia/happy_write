## 组件

> 定义：组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素， Vue.js 的编译器为它添加特殊功能。在有些情况下，组件也可以是原生 HTML 元素的形式，以 is 特性扩展。

```javascript
option={
	props: ['',''], //父组件通过props传递参数给子组件,注意当父组件的prop值为`my-prop`时子组件会自动转化为`myProp`
	template: '<div></div>',
	data: factory, //data必须为函数
}
```

* 注册一个全局组件：`Vue.component('tagName',option);`
* 注册局部组件：
```javascript
new Vue({
	el:'',
	components: {
		'tagName': {
			template: '<div>内容</div>'
		}
	}
});
```

### DOM解析注意

> `<ul>`、`<ol>`、`<table>`、`<select>` 限制了被包裹的元素类型，隐藏用自定义组件放进去会导致浏览器报错。可通过is特性解决该问题。

```javascript
// 报错
<table>
  <my-row>...</my-row>
</table>
```
```javascript
// 解决方法
<table>
  <tr is="my-row"></tr>
</table>
```

