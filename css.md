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
3. css获取`第一个子元素`、`倒数第二个子元素`、`倒数第一个子元素`
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
4. 设置div 水平垂直居中的方法
```css
/* 1.transform 不确定宽高时  */
div {
	postion: absoulte;
	top: 50%;
	left: 50;
	transform: translate(-50%, -50%);
}
/* 2. flex布局 */
.box {
	display: flex;
	align-items: center;
	justify-content: center;
}
/* 3. margin:auto 需要确定容器宽高 */
.box {
	position: relative;
}
div {
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	width: 100px;
	height: 100px;
	margin: auto;
}
```
5. `flex: 1`的是什么的缩写
> 1. flex-grow 默认是0，表示不做内容扩展
> 2. flex-shrink 默认是1，表示宽高不够时会缩小
> 3. flex-basis