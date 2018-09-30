---
layout: post
title:  "Welcome to Jekyll!"
date:   2018-07-26 13:31:01 +0800
categories: CSS
tag: ''
---

<p>1.与javascript共享变量</p>
<pre>
	<code>
/*config.scss*/
$color:"F00";
:export{
	color:$color;
}

/*app.js*/
import styles from 'config.scss';
/*会打印出"F00"*/
console.log(styles.color)
	</code>
</pre>

<p>2.获取全局样式</p>
<p>cssModule自动给class名外加了:local,以此来实现样式的局部化</p>
<pre><code>
/*获取局部类名*/
.normal{
	
}
:local(.normal){
	
}

/*获取全局类名*/
:global(.normal){
	
}

/*获取多个全局类名*/
:global{
	.normal{

	}
	.active{

	}
}
</code></pre>

<p>3.添加多个类名</p>
<pre><code>
/*config.scss*/
.normal{
	color:blue;
	width:100px;
}
.emphsis{
	color:red;
	width:150px;
}
:global(.active){
	width:200px;
}

/*app.js*/
import styles from 'config.scss';
/*此时的最终样式为{width:"200px", color:"red"}*/
<button style={styles.normal +" "+ styles.emphsis +" active"}></button>
</code></pre>

<p>4.外部覆盖局部样式</p>
<p>由于生成样式时会自动添加前缀和后缀来进行混淆已保证类名不会冲突，有时会有父组件控制子组件样式的需求(具体好像没啥用)。样式无法覆盖，父组件只能控制子组件未控制的样式</p>
<pre><code>
/*chilren.js*/
<div data-role="children"></div>
/*parent.less*/
[data-role="children"]{
	width:300px;
}
</code></pre>

<p>与全局样式共存</p>