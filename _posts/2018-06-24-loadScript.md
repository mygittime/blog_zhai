---
layout: post
title:  同一页面多个模块需要依赖相同js文件的解决方案
date:   2018-06-24 00:00:00 +0800
categories: ""
tag: ""
---

<p>最近参与了一个项目，项目中使用了大量的zrender和echarts编写的图表，简单来讲，可以使用script的onload方法来控制渲染。但实际项目中情况比较复杂，所以需要封装一个加载js的方法</p>
<pre>
	<code>
//总体思路，每个文件都有一个promise，加载新文件时，有promise就等待promise，无promise就创建新的promise

//每加载一个图表就存一次全局变量,加载新的js时先在全局变量里找
//文件有四种状态
//1.未加载，说明需要加载  !window.loadScript[name] == true
//2.加载完成，window.loadScript[name] == 'loaded';
//3.加载失败，window.loadScript[name] == 'failed';目前发现失败无任何操作
//4.加载中，让新的promise也进入等待状态 ,判断条件为不同于上面三种情况
function loadScript(name, url){	
	if(!window.loadScript){
		window.loadScript = {};
	}

	//多个js文件,将加载中和未加载的文件挑出来
	//未加载的文件把文件名和路径放入数组
	//加载中的文件将promise放入数组
	//传给加载多个文件的方法
	if(name instanceof Array){
		//把需要加载的js文件挑出来
		let needLoadScript = [];
		for(let i=0;i<name.length;i++){
			if(!window.loadScript[name[i]] ){//未找到文件
				needLoadScript.push(loadingSingleScript(name[i], url[i]));
			}else{//文件正在加载或已加载完成
				if(window.loadScript[name] == 'loaded'){//文件已加载完成

				}else if(window.loadScript[name] == 'failed'){//文件加载失败，尝试重新加载
					needLoadScript.push(loadingSingleScript(name[i], url[i]));
				}else{//文件正在加载
					needLoadScript.push(window.loadScript[name[i]])
				}
			}
		}
		//文件已存在，不进行重新加载
		if(needLoadScript.length == 0){
			return Promise.resolve('文件已存在')
		}else if(needLoadScript.length == 1){
			return needLoadScript[0];
		}else{
			return loadMultipleScript(needLoadScript);
		}
		

	//加载单个文件
	//文件未加载就开始加载
	//文件加载中
	}else{
		let loadScript = window.loadScript;
		if(!loadScript[name]){//文件未加载
			return loadingSingleScript(name, url);
		}else{
			if(loadScript[name] == 'loaded'){//文件已经存在
				return Promise.resolve(name+'文件已存在')
			}else if(loadScript[name] == 'failed'){//文件加载失败
				console.log(name+'加载失败，并且不会再次加载');
				return Promise.reject(name+'加载失败，并且不会再次加载')
			}else{//文件加载中
				return loadScript[name];
			}	
			
		}
	}
}

//同时加载多个js
function loadMultipleScript(scripts){
	return (
		Promise.all(scripts)
			.then(()=>{
				for(let i=0;i<scripts.length;i++){
					window.loadScript[scripts[i]] = 'loaded';
				}
			})
	)
}

//加载单个js
function loadingSingleScript(name, url){
	let promise = new Promise((resolve, reject) => {
					let newScript = document.createElement('script') ;
					newScript.src = url;
					newScript.type = 'text/javascript';
					document.body.appendChild(newScript);
					newScript.onload = () => {
						window.loadScript[name] = 'loaded';
						resolve(url +'加载成功');
					}
					newScript.onerror = () => {
						window.loadScript[name] = 'failed';
						reject(url +'加载失败');
					}
				})
	window.loadScript[name] = promise;
	
	return 	window.loadScript[name];
}

export {loadScript};
	</code>
</pre>

<h3>使用方法如下：</h3>
<p>加载单个js文件</p>
<pre><code>
import {loadScript} from url;
loadScript(name,url).then(resp=>{
	//渲染图表
})
</code></pre>
<p>加载多个js文件</p>
<pre><code>
import {loadScript} from url;
loadScript([name],[url]).then(resp=>{
	//渲染图表
})
</code></pre>

<h3>如果像我一样，在项目中，还需要先加载固定的几个第三方依赖js，可以进行如下修改：</h3>
<pre><code>
//添加一个新的方法并进行暴露
function loadDependScript(){
	let name = ['TweenMax.min.js', 'zrender.min.js', 'three.min.js'];
	let url = ['/depend/TweenMax.min.js', '/depend/zrender.min.js', '/depend/three.min.js'];
	return loadScript(name, url)
}
export {loadScript, loadDependScript};
</code></pre>
<h3>使用方法如下：</h3>
<pre><code>
import {loadScript, loadDependScript} from url;
loadDependScript().then(resp => {
	loadScript(name,url).then(resp => {
		//渲染图表
	})
})
</code></pre>