## 1 first-child 与 first-of-type ##
	<div class="parent">
		<h4>我是parent中的h4</h4>
		<p>我是parent中第一个p</p>
		<p>我是parent中第二个p</p>
		...很多p标签
	</div>
<p>上面一段代码，如果想让第一个p标签高亮，不少人很可能用first-child属性 如 
p:first-child{color:red}
</p>
<p>本以为上面的代码可以实现，结果却是没影响</p>
<div class="d1" style="margin-left:100px">
	<h4>我是d1中的h4</h4>
	<p>我是d1中第一个p</p>
	<p>我是d1中第二个p</p>
	...很多p标签
</div>
<hr>
<p style="color: purple;font-size:20px">
p:first-child的含义
<br>
1 找到p标签的父级元素
<br>
2 它父级元素所对应的第一个子节点
<br>
3 第一个子节点要是对应的标签或类（p标签）
</p>
<hr>
解决方法有多中，可以加class等等，但是如果是动态的数据推荐使用first-of-type
<br>
<p style="color: blue;font-size:20px">
	p:first-of-type的含义
	<br>
	1 找到p标签的父级元素
	<br>
	2 它父级元素所有的是p标签的子节点
	<br>
	3 选出子节点第一个的标签或类（p标签）
</p>

结果
<br>
<style>
	.d2{margin-left:100px}
	.d2 p:first-of-type{color:red}
</style>
<div class="d2">
	<h4>我是d2中的h4</h4>
	<p>我是d2中第一个p</p>
	<p>我是d2中第二个p</p>
	...很多p标签
</div>
<hr>
<p style="font-size: 18px; font-weight:bold">
	类似的还有last-child（last-of-type）,nth-last-child（nth-last-of-type）,nth-child（nth-of-type）等
</p>
<hr>
## 2 margin-top ##
看下面的代码

	.container
	{
		width: 400px;
		height: 200px;
		border: 1px solid #000;
	}
	.parent
	{
		width: 100px;
		height: 100px;
		background-color: yellow;
	}
	.firstChild
	{
		width: 20px;
		height: 20px;
		background-color: red;
		margin-top: 20px;
	}
	<div class="container">
		<div class="parent">
			<div class="firstChild"></div>
		</div>
	</div>

期待的结果是<br>
<style>
	.container0
	{
		width: 400px;
		height: 200px;
		border: 1px solid #000;
	}
	.parent0
	{
		width: 100px;
		height: 100px;
		overflow: hidden;
		background-color: yellow;
	}
	.firstChild0
	{
		width: 20px;
		height: 20px;
		background-color: red;
		margin-top: 20px;
	}
</style>
<div class="container">
	<div class="parent0">
		<div class="firstChild0"></div>
	</div>
</div>
</div>
实际的结果却是<br>
<style>
	.container
	{
		width: 400px;
		height: 200px;
		border: 1px solid #000;
	}
	.parent
	{
		width: 100px;
		height: 100px;
		background-color: yellow;
	}
	.firstChild
	{
		width: 20px;
		height: 20px;
		background-color: red;
		margin-top: 20px;
	}
</style>
<div class="container">
	<div class="parent">
		<div class="firstChild"></div>
	</div>
</div>
<hr>
<p>出现这种现象的原因是</p>
<p style="color: #00f;font-size:20px">一个盒子如果没有上补白(padding-top)和上边框(border-top)，那么这个盒子的上边距会和其内部文档流中的第一个子元素的上边距重叠。<br>也就是说第一个元素的margin-top属性具有传递性（父级元素也具有相同的属性）</p>
<hr>
<p>解决方法也有很多种</p>
<h4>a.父级元素加overflow:hidden</h4>
<style>
	.container1
	{
		width: 400px;
		height: 200px;
		border: 1px solid #000;
	}
	.parent1
	{
		width: 100px;
		height: 100px;
		overflow: hidden;
		background-color: yellow;
	}
	.firstChild1
	{
		width: 20px;
		height: 20px;
		background-color: red;
		margin-top: 20px;
	}
</style>
<div class="container1">
	<div class="parent1">
		<div class="firstChild1"></div>
	</div>
</div>
<h4>b.父级元素加个透明的border-top  border-top: 1px solid transparent;</h4>
<style>
	.container2
	{
		width: 400px;
		height: 200px;
		border: 1px solid #000;
	}
	.parent2
	{
		width: 100px;
		height: 100px;
		border-top: 1px solid transparent;
		background-color: yellow;
	}
	.firstChild2
	{
		width: 20px;
		height: 20px;
		background-color: red;
		margin-top: 20px;
	}
</style>
<div class="container2">
	<div class="parent2">
		<div class="firstChild2"></div>
	</div>
</div>
<h4>c.父级元素浮动 float: left;</h4>
<style>
	.container3
	{
		width: 400px;
		height: 200px;
		border: 1px solid #000;
	}
	.parent3
	{
		width: 100px;
		height: 100px;
		float: left;
		background-color: yellow;
	}
	.firstChild3
	{
		width: 20px;
		height: 20px;
		background-color: red;
		margin-top: 20px;
	}
</style>
<div class="container3">
	<div class="parent3">
		<div class="firstChild3"></div>
	</div>
</div>
<h4>d.第一个子元素前增加一个1*1的元素</h4>
<style>
	.container4
	{
		width: 400px;
		height: 200px;
		border: 1px solid #000;
	}
	.parent4
	{
		width: 100px;
		height: 100px;
		background-color: yellow;
	}
	.addChild4
	{
		width: 1px;
		height: 1px;
	}
	.firstChild4
	{
		width: 20px;
		height: 20px;
		background-color: red;
		margin-top: 20px;
	}
</style>
<div class="container4">
	<div class="parent4">
		<div class="addChild4"></div>
		<div class="firstChild4"></div>
	</div>
</div>