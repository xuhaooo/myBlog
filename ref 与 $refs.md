# Vue2 API 之 ref 与 $refs

> `ref`，值是一个字符串，被用来给元素或者子组件注册引用信息，注册信息将会注册到父组件的 `$refs` 对象上。如果在普通 DOM 元素上使用，引用指向的就是该 DOM 元素；如果使用在子组件上，引用指向组件实例
> 

> `$refs`，是一个对象，持有注册过 `ref` 的所有 DOM 元素和组件实例
> 

## 使用场景

### 1. 获取 DOM 元素

```jsx
<div id="app">
	<p ref="msg">{{ msg }}</p>
	<span ref="item">{{ item }}</span>
	<button @clcik="click">点击</button>
</div>

new Vue({
	el: '#app',
	data: {
		msg: 'hello world',
		item: 'awesome vue'
	},
	methods: {
		click(){
			console.log(this.$refs) // {msg: p, item: span}
			console.log(this.$refs.msg) // <p>hello world</p>
			console.log(this.$refs.item) // <span>awesome vue</span>
			console.log(this.$refs.msg.innerHTML) // hello world
		}
	}
})
```

### 2. 获取子组件的 `data`

```jsx
<div id="app">
	<child ref="child"></child>
</div>

const child = {
	template: '<div>{{msg}}</div>',
	data(){
		return {
			msg: '我是子组件'
		}
	}
}

new Vue({
	el: '#app',
	mounted(){
		console.log(this.$refs.child.msg) // 我是子组件
	},
	components: {
		child
	}
})
```

### 3. 调用子组件中的方法

```jsx
<div id="app">
	<child ref="child"></child>
</div>

const child = {
	template: '<div>我是子组件</div>',
	methods: {
		sayHi(){
			console.log('hi')
		}
	}
}

new Vue({
	el: '#app',
	mounted(){
		console.log(this.$refs.child.sayHi()) // hi
	},
	components: {
		child
	}
})
```

### 4. `ref` 与 `v-for` 一起使用

> 当 `v-for` 用于元素或组件时，引用信息将包含 DOM 节点或组件实例的数组
> 

```jsx
<div id="app">
	<div v-for="item in 8" :key="item" ref="item">{{item}}</div>
</div>

new Vue({
	el: '#app',
	mounted(){
		console.log(this.$refs) // {item: Array(8)}
		console.log(this.$refs.item) // [div, div, div, div, div, div, div, div]
		console.log(this.$refs.item[0]) // <div>1</div>
	}
})
```

## 注意事项

> 由于 `ref` 本身是作为渲染结果被创建的，在初识渲染的时候你不能访问它，因为它还不存在；`$refs` 也不是响应式的，所以你也不应该视图用它在模板中做数据绑定
> 

可是有的时候，我们需要使用 `this.$refs` 来获取某些动态渲染的元素

由于，使用 `this.$refs` 的时候，动态绑定的 DOM 元素还没有初始化

这时，我们可是使用`this.$nextTick()` 来让回调延迟到 DOM 更新之后执行，这样就可以获取到这些元素了