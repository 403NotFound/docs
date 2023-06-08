## CSS

### 1. margin重叠问题？如何解决？

在纵向相邻的元素的垂直方向上的margin会发生重叠，可以创建BFC使这两个相邻的元素处于不同的BFC来解决这个问题。

### 2. margin负值问题

- top负值，元素自身向上移动
- left负值，元素自身向左移动
- right负值，元素自身不动，元素右边的元素向左移动
- bottom负值，元素自身不定，元素下方的元素向上移动

### 3. 什么是BFC，对BFC的理解和应用？

**块格式化上下文**（Block Formatting Context，BFC）是 Web 页面的可视 CSS 渲染的一部分，是块级盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。

下列方式会创建块格式化上下文：

- 根元素（`<html>`）
- 浮动元素（[`float`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/float) 值不为 `none`）
- 绝对定位元素（[`position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position) 值为 `absolute` 或 `fixed`）
- 行内块元素（[`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 值为 `inline-block`）
- 表格单元格（[`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 值为 `table-cell`，HTML 表格单元格默认值）
- 表格标题（[`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 值为 `table-caption`，HTML 表格标题默认值）
- 匿名表格单元格元素（[`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 值为 `table`、`table-row`、 `table-row-group`、`table-header-group`、`table-footer-group`（分别是 HTML table、tr、tbody、thead、tfoot 的默认值）或 `inline-table`）
- [`overflow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow) 值不为 `visible`、`clip` 的块元素
- [`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 值为 `flow-root` 的元素
- [`contain`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/contain) 值为 `layout`、`content` 或 `paint` 的元素
- 弹性元素（[`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 值为 `flex` 或 `inline-flex` 元素的直接子元素），如果它们本身既不是 [flex](https://developer.mozilla.org/zh-CN/docs/Glossary/Flex_Container)、[grid](https://developer.mozilla.org/zh-CN/docs/Glossary/Grid_Container) 也不是 [table](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_table) 容器
- 网格元素（[`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display) 值为 `grid` 或 `inline-grid` 元素的直接子元素），如果它们本身既不是 [flex](https://developer.mozilla.org/zh-CN/docs/Glossary/Flex_Container)、[grid](https://developer.mozilla.org/zh-CN/docs/Glossary/Grid_Container) 也不是 [table](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_table) 容器
- 多列容器（[`column-count`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/column-count) 或 [`column-width` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/column-width) 值不为 `auto`，包括`column-count` 为 `1`）
- `column-span` 值为 `all` 的元素始终会创建一个新的 BFC，即使该元素没有包裹在一个多列容器中 ([规范变更](https://github.com/w3c/csswg-drafts/commit/a8634b96900279916bd6c505fda88dda71d8ec51), [Chrome bug](https://bugs.chromium.org/p/chromium/issues/detail?id=709362))

格式化上下文影响布局，通常，我们会为定位和清除浮动创建新的 BFC，而不是更改布局，因为它将：

- 包含内部浮动
- 排除外部浮动
- 阻止 [外边距重叠](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing)

### 4. 如何实现圣杯布局和双飞翼布局？

经典的三列布局之圣杯&双飞翼

**圣杯布局：**

```html
<body>
    <div class="wrap">
        <div class="content">
            content
        </div>
        <div class="left">left</div>
        <div class="right">right</div>
    </div>
    
</body>
```

```css
*{
      margin: 0px;
      padding: 0px;
  }
  .content{
      width: 100%;
      background: green;
      height: 200px;
  }
  .left, .right{
      height: 200px;
      width: 200px;
      background: pink;
  }
  .wrap div{
      float: left;
  }
  .wrap{
      padding: 0 200px;
      height: 2000px;
  }
  .left{
  margin-left: -100%;
      position: relative;
      left: -200px;

  }
  .right{
      margin-left: -200px;
      position: relative;
      left: 200px;
  }
```

**双飞翼布局：**

```html
<body>
    <div class="wrap">
        <div class="content">
            <div class="ineer">content</div>
        </div>
        <div class="left">left</div>
        <div class="right">right</div>
    </div>
</body>
```

```css
*{
      margin: 0;padding: 0;
  }
  .left, .right{
      width: 200px;
      height: 200px;
      background:  pink;
      float: left;
  }
  .content{
      height: 200px;
      background: rgb(45, 173, 75);
      float: left;
      width: 100%;
  }
  .ineer{
      margin: 0 200px;
      height: 200px;
  }
  .left{
      margin-left: -100%;
  }
  .right{
      margin-left: -200px;
  }

```



### 5. flex: 1是什么意思？

- flex-grow: 1
- flex-shrink: 1
- flex-basis: 0%

### 6. 如何实现水平居中对齐？

```html
<div class="box1">
    <div></div>
</div>
```

**不知道元素宽高：**

```css
/************方案一*****************/
.box1 {
    position: relative;
}
.box1 div {
    position: absolute;
    top: 50%;
    left: 50%;
    /*transform:translate(x,y)括号的百分比数据，会以本身的长宽做参考*/
    transform: translate(-50%,-50%);
}
/************方案二*****************/
.box1 {
    position: relative;
}
.box1 div {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
}
/************方案三*****************/
.box1 {
    display: flex;
    justify-content: center;
    align-items: center;
}
/************方案四*****************/
.box1 {
    display: table-cell;
    vertical-align: middle;
    text-align: center;
}
.box1 div {
    display: inline-block;
}
```

**已知元素宽高（上述方案同样适用）：**

```css
.box1 {
    position: relative;
}
.box1 div {
    width: 100px;
    height: 100px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -50px;/*负的高度的一半*/
    margin-left: -50px;/*负的宽度的一半*/
}
```

### 7. line-height如何继承？



### 8. 如何实现响应式布局？



### 9. 分析比较 *opacity: 0、visibility: hidden、display: none* 优劣和适用场景？



### 10. 如何用 css 或 js 实现多行文本溢出省略效果，考虑兼容性



### 11. 居中为什么要使用 *transform*（为什么不使用 *marginLeft/Top*）



### 12. 什么是粘性布局（sticky）?



### 13. 说出 `space-between` 和 `space-around`的区别？



### 14. *CSS3* 中 `transition和` `animation` 的属性分别有哪些?



### 15. 如何实现一个自适应的正方形？



### 16. 如何清除浮动？



### 17. 重绘和重排的区别？



### 18. 什么是渐进增强和优雅降级？



### 19. CSS3新增了哪些东西？



### 20. 如何隐藏一个元素，请说出几种方案？



