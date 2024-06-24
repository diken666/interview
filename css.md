# css

1. chorme浏览器如何显示12px以下
```css
span {
	zoom: 0.8;
	// 或者
	transform: scale(0.8);
}
```
2. 英文首字母大写
```css
span {
	text-transform: capitalize; // uppercase全大写 lowercase全小写
}
```
=======
1. css获取`第一个子元素``倒数第二个子元素``倒数第一个子元素`
```html
<div>
	<p>1</p>
  <p>2</p>
  <p>3</p>
  <p>4</p>
  <p>5</p>
</div>	
```
```css
div p:nth-child(1) {}
div p:nth-last-child(2) {}
div p:last-child {}
```
>>>>>>> 0d7d4da851aa62e8336e3596901441c73065ee5b
