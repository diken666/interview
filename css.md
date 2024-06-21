# css
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