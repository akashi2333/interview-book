# HTML节点操作

在DOM中，每一个节点都是一个对象。DOM节点有三个重要的属性：

- nodeValue：节点的值。
- nodeName：节点的名称。
- nodeType：节点的类型（元素、属性、文本、注释、整个文档）。

![](https://img2018.cnblogs.com/i-beta/1226410/201912/1226410-20191231100910404-878474224.png)

## 添加节点

```
<div id="div1">
	<p id="p1">这是一个段落。</p>
	<p id="p2">这是另一个段落。</p>
</div>
<script>
    var para=document.createElement("p");
    var node=document.createTextNode("这是一个新段落。");
    para.appendChild(node);
    var element=document.getElementById("div1");
    element.appendChild(para);
</script>
```

## 删除节点

```
<div id="t3">
    <div>下边的兄弟被删除了</div>
    <div>我要被删除了</div>
</div>
<script type="text/javascript">
    document.getElementById("t3").removeChild(document.querySelector("#t3 > div:nth-child(2)"));
</script>
```

## 替换节点

```
<div id="t2">
	<div>被替换的节点</div>
</div>
<script type="text/javascript">
    var d2 = document.createElement("div");
    d2.style.color = "green";
    d2.innerText="被我替换了";
    document.getElementById("t2").replaceChild(d2,document.querySelector("#t2 > div:first-child")); // 第一个参数是要替换的节点，第二个参数是被替换的节点
</script>
```

## 绑定事件

```
<div id="t4" style="color: red;">点我</div>
<script type="text/javascript">
	document.getElementById("t4").addEventListener('click',(e) => {
            alert("点击事件");
    })   
</script>
```

## 访问子节点

```
<div id="t5" style="color: grey;">
	<div>1</div>
    <div>2</div>
</div>
<script type="text/javascript">
	console.log(document.getElementById("t5").childNodes); // 获取所有子节点 // 注意每个换行也会有一个#text文本节点
    console.log(document.getElementById("t5").childElementCount); // 获取子节点数量
    console.log( document.getElementById("t5").firstChild); // 获取第一个子节点，注意也会匹配#text
    console.log(document.getElementById("t5").firstElementChild); // 获取第一个子节点
    console.log(document.getElementById("t5").lastChild); // 获取最后一个子节点，注意也会匹配#text
    console.log(document.getElementById("t5").lastElementChild); // 获取最后一个子节点
</script>
```

## 访问父节点

```
<div style="color: yellow;">
    <div id="t6">1</div>
</div>
<script type="text/javascript">
	console.log(document.getElementById("t6").parentNode);
</script>
```

## 访问兄弟节点

```
<div style="color: brown;">
	<div>1</div>
	<div id="t7">2</div>
	<div>3</div>
</div>
<script type="text/javascript">
	console.log(document.getElementById("t7").previousSibling); // 注意也会匹配#text
    console.log(document.getElementById("t7").previousElementSibling); // 不匹配文本节点、注释节点
    console.log(document.getElementById("t7").nextSibling); // 注意也会匹配#text
    console.log(document.getElementById("t7").nextElementSibling); // 不匹配文本节点、注释节点
</script>
```

