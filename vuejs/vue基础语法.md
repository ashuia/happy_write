## 模板语法

1. 文本绑定
> `<span v-once>This will never change: {{ msg }}</span>`
> `v-once` 指只插值一次

2. html绑定
> '<div v-html="rawHtml"></div>'

3. 属性绑定
> `<div v-bind:id="dynamicId"></div>`

4. `javascript` 表达式,每个绑定都只能包含单个表达式
> `{{ message.split('').reverse().join('') }}` :heavy_check_mark:
> `{{ ok ? 'YES' : 'NO' }}` :heavy_check_mark:
> `{{ number + 1 }}` :heavy_check_mark:
> `{{ var a = 1 }} <!-- 这是语句，不是表达式 -->` :x:
> `{{ if (ok) { return message } }} <!-- 流控制也不会生效，请使用三元表达式 -->` :x:

5. 指令
> `<p v-if="seen">Now you see me</p>` `v-if`指令根据表达式真假判断是否执行，这里是判断是否插入
> `<a v-bind:href="url"></a>` `v-bind`指令绑定指定的参数
> `<a v-on:click="doSomething">` `v-on`指令绑定事件

6. 特殊绑定
> `<form v-on:submit.prevent="onSubmit"></form>` '.prevent'表示对于触发的事件调用'event.preventDefault()'

7. 缩写
> `v-on`缩写: `<a v-on:click="doSomething"></a>` 可缩写成 `<a @click="doSomething"></a>`
> 'v-bind'缩写: `<a v-bind:href="url"></a>` 可缩写成 `<a :href="url"></a>`

8. 过滤器
> 过滤器只能在 `mustache` 绑定和 `v-bind` 表达式（从 2.1.0 开始支持）中使用,且过滤器函数总接受表达式的值作为第一个参数。也就是通过管道符 `|` 将前一个的表达式的值传给当前过滤器函数。
```javascript
<div id="demo">
	{{ haha | hehe | hahe(5, 3) }} //此时输出 13
</div>
var app = new Vue({
	el: '#demo',
	data:{
		haha: 'nihao'
	},
	filters: {
		hehe: function (value){
			return value.length;
		},
		hahe: function (value, one, two){ //注意：第一个参数总是前一个表达式的执行结果
			return value + one + two;
		}
	}
})
```

## 计算属性

> **计算属性与方法属性的对比**：计算属性保留计算缓存，方法属性没有。当遇到多次的高计算量的计算时用计算属性比用方法属性高效。
```javascript
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
  <p>Reversed message: "{{ reversedMsg() }}"</p>
</div>
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    }
  },
  methods: {
    reversedMsg: function () {
      return this.message.split('').reverse().join('')
    }
  }
});
```

> **计算属性与观察属性**：观察属性绑定指定变量，并捕捉这个变量的变化触发相应函数。计算属性似乎包含了观察属性的特性，功力不佳，以后回看。:bangbang:
```html
<div id="demo">{{ fullName }}</div>
```

```javascript
var vm = new Vue({ //观察属性方法
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName;
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val;
    }
  }
});
// 可见观察属性通过捕捉变量的变化来改变fullName的值。
```

```javascript
var vm = new Vue({ //计算属性方法
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName;
    }
  }
});
// 通过试验，可以达到相同的效果，且计算属性的代码更简洁高效。
```

```javascript
// 通过设置`setter + getter`达到firstName、lastName与fullName的双向绑定
var vm = new Vue({
	el: '#demo',
	data: {
		firstName: 'Foo',
		lastName: 'Bar'
	},
	computed: {
		fullName: {
			get: function (){
				return this.firstName + ' ' + this.lastName;
			},
			set: function (newValue){
				var names = newValue.split(' ');
				this.firstName = names[0];
				this.lastName = names[1];
			}
		}
	}
});
```

## `Class` 与 `Style` 绑定

> 用`v-bind`命令实现`class`的绑定
```javascript
// **对象形式**, 属性值为true是加入
<div v-bind:class="classObject"></div>
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
// 解析后
<div class="active"></div>

// **数组形式**
<div v-bind:class="[activeClass, errorClass]">
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
// 渲染后
<div class="active text-danger"></div>
```

> 用`v-bind`命令实现`style`的绑定

```javascript
// **直接传入对象**
<div v-bind:style="styleObject"></div>
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
// 数组方式每一个成员对应相应的对象
<div v-bind:style="[baseStyles, overridingStyles]">
```

## 条件渲染

> v-if与v-show的区别,前者是真实的条件渲染，后者只是修改display达到显示与隐藏

```javascript
<div v-if="step === 'one'">haha</div>
<div v-else-if="step === 'two'">haha</div>
<div v-else>hahe</div>
```

## 列表渲染

> `v-for='( (item, key, index) in items )';` //获取对象items里的值，item为值，key为键，index为索引

数组方法
	push() //末尾推进一项
	pop() //末尾推出一项
	shift() //首部推出一项
	unshift() //首部推进一项
	splice() //
	sort() //重排序
	reverse() //倒序

#### 注意事项

> 由于 `JavaScript` 的限制， `Vue` 不能检测以下变动的数组：

1. 当你利用索引直接设置一个项时，例如： `vm.items[indexOfItem] = newValue`
	```javascript
	// Vue.set
	Vue.set(example1.items, indexOfItem, newValue)
	// Array.prototype.splice`
	example1.items.splice(indexOfItem, 1, newValue)
	```
2. 当你修改数组的长度时，例如： `vm.items.length = newLength`
	```javascript
	example1.items.splice(newLength)
	```