# 浅析 Vue 数据响应式

> Vue 框架的核心之一就是它能实现数据响应式。什么响应式，响应式是一个模糊的概念，只要你对我的操作做出了反应，那么你就是响应式的。而在 Vue 中，当我们改变了数据时，UI 会更新并做出相应的改变。这里，我们来分析一下 Vue 的数据响应式背后的秘密。
> 

# 一、从一个小实验开始

```jsx
// main.js
const myData = {
  n: 0
}

new Vue({
  data: myData,
  template: `
    <div>{{n}}</div>
  `
}).$mount("#app");

setTimeout(()=>{
  myData.n += 10
  console.log(myData)
},3000)
```

我们通过上面这段代码看一下 data 在 3s 之后的变化，在控制台中查看输出的结果。我在查看之前，认为输出的结果应该是这样的：

```jsx
{n: 0}
{n: 10}
```

而实际的结果却是这样的：

```jsx
{n: 0}
{n: (...)}
```

这个 `{n: (...)}` 是什么东西？为什么 3s 之后控制台输出的结果是这样的？

请带着这个疑惑继续看下去

# 二、与杠精的较量

```jsx
let data0 = {
	n: 0
}
```

## 1. 杠精需求 一：用一个 Object.defineProperty 定义 n

这很简单啊

```jsx
let data1 = {}
Object.defineProperty(data1, 'n', {
	value: 0
})

console.log(`需求一：${data1.n}`)
// 需求一：0
```

## 2. 杠精需求二：n 不能小于 0

这也很简单啊

```jsx
let data2 = {}
data2._n = 0

Object.defineProperty(data2, 'n', {
	get(){
		return this._n
	},
	set(value){
		if(value < 0){
			return
		}else{
			this._n = value
		}
	}
})

console.log(`需求二：${data2.n}`)
data2.n = -1
console.log(`需求二：${data2.n} 设置为 -1 失败`)
data2.n = 1
console.log(`需求二：${data2.n} 设置为 1 成功`)
// 需求二：0
// 需求二：0 设置为 -1 失败
// 需求二：1 设置为 1 成功
```

这里使用 `_n` 来存储 `n` 的值，通过数据劫持的方式，使得 `n` 无法被设置为小于 0 的值。

## 3. 抬杠：那我直接使用 data._n 呢？

这样你就无法完成需求二了

```jsx
let data3 = proxy({ data:{n:0} })

function proxy({data}){
  const obj = {}

  Object.defineProperty(obj, 'n', { 
    get(){
      return data.n
    },
    set(value){
      if(value < 0){
				return
			}else{
	      data.n = value
			}
    }
  })
  return obj
}

console.log(`需求三：${data3.n}`)
data3.n = -1
console.log(`需求三：${data3.n}，设置为 -1 失败`)
data3.n = 1
console.log(`需求三：${data3.n}，设置为 1 成功`)
// 需求三：0
// 需求三：0，设置为 -1 失败
// 需求三：1，设置为 1 成功
```

`proxy({ data: {n: 0} })` 这里面实际上是匿名对象 `{n: 0}` ，`data` 是为了后面解释的需要，可以忽略。

另外，这里的 'n' 写死了，理论上应该遍历 data 的所有 key，这里做了简化。

这里是使用代理的方式，让 `data3` 成为 `{n: 0}` 的代理，你想对数据做的任何操作，都需要先经过我的代理 `data3`，没有再暴露出类似 `_n` 这样的变量，供杠精去修改我的数据。

## 4. 杠精：我还能杠

我可以使用一个变量 `myData` 去引用你的匿名数据对象 `{n: 0}`，然后将 `myData` 传给你的代理函数，这样我就可以绕过你的代理去直接修改你的数据

```jsx
let myData = {n: 0}
let data4 = proxy({ data: myData })

console.log(`杠精：${data4.n}`)
myData.n = -1
console.log(`杠精：${data4.n}，设置为 -1 失败了吗!?`)
```

好呀，你以为我没招了是吧，就算你像这样，我还是可以拦截你！

我要升级我的代理函数

```jsx
let myData5 = {n :0}
let data5 = proxy2({ data: myData5 })

function proxy2({data}){
  let value = data.n
  Object.defineProperty(data, 'n', {
    get(){
      return value
    },
    set(newValue){
      if(newValue < 0){
        return
      }else{
        value = newValue
      }
    }
  })

  const obj = {}
  Object.defineProperty(obj, 'n', {
    get(){
      return data.n
    },
    set(value){
      if(value < 0){
        return
      }else{
        data.n = value
      }
    }
  })
  return obj
}

console.log(`需求五：${data5.n}`)
myData5.n = -1
console.log(`需求五：${data5.n}，设置为 -1 失败了`)
myData5.n = 1
console.log(`需求五：${data5.n}，设置为 1 成功了`)
```

使用代理函数对数据对象 `{n: 0}` 进行了代理，所有的对数据对象的读写必须经过我的代理对象 `data5` ，杠精无法直接对我的数据对象进行操作。另外我在代理函数中对数据 `n` 进行了劫持，将真实的数据赋值给了 `value`，并对 `n` 进行了设置，这样即使杠精使用变量 `myData5` 引用 `{n: 0}`，也无法做到直接修改我的数据。至此，我就可以做到 100% 地防止杠精在我不知道的情况下去修改数据。

# 三、回答小实验的疑问

可能经过了上面的『与杠精的较量』之后，你会问：这与上面的小实验产生的疑问有什么关系呢？别着急，先看看下面的两行代码：

```jsx
let data5 = proxy2({ data:myData5 }) 
let vm = new Vue({data: myData})
```

这两行代码是不是非常的相似，是的，`data5` 是不是就是 `vm`，`proxy2` 是不是就是 `new Vue` 。好，我们来看一下 Vue 到底对 `data` 做了什么？

## 1. Vue 对 data 做了什么

当我们写下 `new Vue({data: myData})`

1. Vue 会让 `vm` 成为 `myData` 的代理，而 `this` 就是 `vm`
2. Vue 会对 `myData` 的所有属性进行监控（劫持）

`vm` 就是 `myData` 的代理，当你使用 `vm` 去 读取或赋值 `n` 的时候，就相当于对 `myData` 进行读取和赋值。你可以使用 `this` 来访问到 `vm`，而声不声明 `vm` 与代不代理无关，只要你写了 `new Vue ({data: myData})` 之后就会产生一个实例，而 `this` 的意义就是在你没有名字的情况下去指代那个对象。

那为什么要对传入的属性进行监控呢？因为 Vue 的功能就是当你在改变数据之后调用 `render(data)` 来帮你更新页面 UI，如果你更改了数据我 Vue 不知道，那你还要我干什么？

这就是 Vue 的数据响应式的由来。

## 2. 关于小实验的疑问

```jsx
const myData = {
  n: 0
}

new Vue({
  data: myData,
  template: `
    <div>{{n}}</div>
  `
}).$mount("#app");

setTimeout(()=>{
  myData.n += 10
  console.log(myData)
},3000)
```

显而易见，3s 后出现的是 `{n: (...)}`，这是因为当 `myData` 传入 `new Vue()`之后，Vue 会对 `myData` 进行了一系列处理，比如进行代理、数据劫持等等。经过 `Object.defineProperty()` 的 `getter`、`setter` 对 `n` 进行了设置，此时的 `n` 已经不再是声明时数据对象里的属性 `n` 了。

# 四、Vue 的数据响应式好像有个 bug

## 1. Object.defineProperty 的问题

```jsx
Object.defineProperty(obj, 'n', descriptor)
```

Vue 中数据响应式的实现是通过 `Object.defineProperty()` 实现对数据的代理和劫持是吧？但是事先如果不传这个 `n` 呢？

```jsx
new Vue({
  data: {},
  template: `
    <div>{{n}}</div>
  `
}).$mount("#app"）
// 警告，会提示 n 没有被定义
// 但是代码会正常执行，只是在渲染的时候页面中没有东西，因为没法在未定义 n 的情况下去使用 n
```

但是我们有一个办法可以绕过这个警告

```jsx
new Vue({
  data: {
    obj: {
      a: 0 // obj.a 会被 Vue 监听 & 代理
    }
  },
  template: `
    <div>
      {{obj.b}}
      <button @click="setB">set b</button>
    </div>
  `,
  methods: {
    setB() {
      this.obj.b = 1 //请问，页面中会显示 1 吗？
    }
  }
}).$mount("#app")
```

页面中不会显示 1，但是我们却绕过了警告。我并没有再数据选项中定义 `b`，但是我却在方法选项中使用了 `b`，然而却没有警告，这是为什么呢？

因为 Vue 的确在会检查 `data` 选项，但是它只会检查第一层，`obj` 已经定义了，那么就把不会警告，当然 `a` 还是会被监听和代理的，只要你写的它都会监听代理。虽然我可以绕过警告，但是这并不是我使用 Vue 的初衷啊。

## 2. 解决办法

### 方法 1：把所有的 key 先声明好

```jsx
data: {
	obj: {
		a: 0,
		b: undefined
	}
}
```

事先将 `key` 声明好，Vue 就会代理并监听它

### 方法 2：使用 Vue.set() 或者 this.$set()

使用 `Vue.set()` 添加了 `b` 属性，之后就可以正常使用了

```jsx
new Vue({
  data: {
    obj: {
      a: 0
    }
  },
  template: `
    <div>
      {{obj.b}}
      <button @click="setB">set b</button>
    </div>
  `,
  methods: {
    setB() {
      Vue.set(this.obj, 'b', 1)
    }
  }
}).$mount("#app")
```

### Vue.set()/this.$set() 的作用

1. 新增 key
    
    不需要我们自己写 `this.obj.b = 1` 这句代码了，Vue 帮我们写
    
2. 自动创建代理和监听
    
    因为之前没有创建过
    
3. 触发 UI 更新
    
    这算是一个副作用，因为一开始是 `undefined`，现在是 1，Vue 就会自动更新 UI，而且这个副作用不是 `Vue.set()` 做的，而是 Vue 做的，但你可以认为是它触发的
    

### 一个例外情况：data 中有数组怎么办

```jsx
new Vue({
  data: {
    array: ["a", "b", "c"]
  },
  template: `
    <div>
      {{array}}
      <button @click="setD">set d</button>
    </div>
  `,
  methods: {
    setD() {
      this.array[3] = "d" //请问，页面中会显示 'd' 吗？
    }
  }
}).$mount("#app")
```

并不会显示 'd'，原因显而易见。但是我们无法提前将数组的所有的 `key` 都提前声明出来，难道我们每次数组操作都要用 `Vue.set()` 或者 `this.$set()` 吗？

[变更方法](https://cn.vuejs.org/v2/guide/list.html#%E5%8F%98%E6%9B%B4%E6%96%B9%E6%B3%95)

Vue 的作者认为，大多数日常的开发过程中，我们操作数组元素并不会通过下标 `this.$set(this.array, 3, 'd')`，而是使用数组的 API `this.array.push('d')`。于是他对数组的 API 进行了篡改，或者说改写。如果我们将数组打印出来 `console.log(this.array)`，会发现原来的处于数组原型链第二层的数组原生 API 比如 `concat`、`push`、`shift` 等，现在处于原型链的三层，而第二层有着 7 个被改写的数组 API，而这 7 个 API 的内部不但继承了原先方法的功能还会帮你去 `Vue.set()` 。