1. 	闭包的定义：一个函数能够访问它外部函数的变量
```js
// 定时器传参
function fun1(a) {
	return function() {
		console.log(a)
	}
}
setTimeout(fun(1), 1000)
```
2. 手写call
```js
let person = {
    getName: function() {
      return this.name
    },
    x: '1'
  }
  let man = {
    name: '章三'
  }
  Function.prototype.myCall = function(context) {
    // 此时this指向getName函数 （谁调用就指向谁）
    if (typeof context !== 'function') {
      throw new Error('this is not a function')
    }
    context = context || window
    context.fn = this
    let resFn = context.fn()
    delete context.fn
    return resFn
  }
  console.log(person.getName.myCall(man))
  console.log(person.x.myCall(man))
```
3. bind、call、apply的区别 [参考](https://vue3js.cn/interview/JavaScript/bind_call_apply.html#%E4%BA%8C%E3%80%81%E5%8C%BA%E5%88%AB)
- 三者都可以改变函数的this对象指向
- 三者第一个参数都是this要指向的对象，如果如果没有这个参数或参数为undefined或null，则默认指向全局window
- 三者都可以传参，但是`apply`是数组，而`call`是参数列表，且`apply`和`call`是一次性传入参数，而`bind`可以分为多次传入
- 三者都可以传参，但是`apply`是数组，而`call`是参数列表，且`apply`和`call`是一次性传入参数，而`bind`可以分为多次传入
```js
// call和apply会立即执行
// call传入的是参数列表
fn.call(obj, 1, 2,3)
// apply传入的是参数数组
fn.apply(obj, [1,2,3])
// bind不会立即执行，传参个call一样
fn.bind(obj, 1,2,3)
```
4. 找出html中所有html标签，并去重
```js
// 当前的所有标签，但此时是类数组
let eleArr = document.querySelector('*')
// 将类数组转化为数组
let tagNameArr = [...eleArr].map(item => item.tagName)
// 用Set来去重，Set也是类数组，将set转化为数组
let res = new Set(tagNameArr)
// 最终结果
[...new Set([...document.querySelector('*')].map(item => item.tagName))]
```
5. 防抖和节流
```js
// 节流: n 秒内只运行一次，若在 n 秒内重复触发，只有一次生效
// 防抖: n 秒后在执行该事件，若在 n 秒内被重复触发，则重新计时
function throttle(fn, delay) {
	let t = true
	return function() {
		if (t) {
			setTimeout(() => {
				fn.apply(this)
				t = true
			}, delay)
		} else {
			t = false
		}
	}
}
function debounce(fn, delay) {
	let t = null
	return function () {
		if (t) {
			clearTimeout(t)
		}
		t = setTimeout(() => {
      fn.apply(this)
    }, delay)
	}
}
```
6. 原型和原型链
> 每一个函数都有一个prototype属性, 它的实例化对象有__proto__属性, proto指向prototype的内容
> prototype 属性指向一个原型对象时，在默认情况下，这个原型对象将会获得一个 constructor 属性，这个属性是一个指针，指向 prototype 所在的函数对象
> https://github.com/CavsZhouyou/Front-End-Interview-Notebook/blob/master/JavaScript/JavaScript.md#1-%E4%BB%8B%E7%BB%8D-js-%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B
> http://cavszhouyou.top/JavaScript%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3%E4%B9%8B%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%8E%9F%E5%9E%8B%E9%93%BE.html

7. `Proxy`代理时为什么要使用`Reflect`？
```js
let user = {
  _name: "Guest",
  get name() {
    return this._name;
  }
};
let userProxy = new Proxy(user, {
  get(target, prop, receiver) {
    return target[prop]; // (*) target = user
  },
  get(target, prop, receiver) {
  	return Reflect.get(...arguments)
  }
});
let admin = {
  __proto__: userProxy,
  _name: "Admin"
};

// 期望输出：Admin
alert(admin.name); // 输出：Guest (?!?)
```

8. `深拷贝`和`浅拷贝`
```js
// 浅拷贝
// 1. Object.assign
let a = { id: 1, name: 'tom' }
let b = Object.assign(a, {})
b.id = 9
a.id // 9
// 2. 展开运算符... （第一层是浅拷贝，第二层是深拷贝）
let b = {...a}
b.id = 9
a.id // 9
// 深拷贝
// 1. JSON.parse 和 JSON.stringify (缺点：不能拷贝RegExp、Date、取不到值为undefined的key、NaN -> null、symbal会丢失)
```
9. 关于`this`运用，写出下列输出
```js
let name = 222
let a = {
	name: 111,
	say: function() {
		console.log(this.name)
	}
}

let fun = a.say
fun()  // a.say.bind(window)
a.say()

let b = {
	name: 333,
	say: function(fn) {
		fn()
	}
}
b.say(a.say)
b.say = a.say
b.say()
```