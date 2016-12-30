* Vue.js是什么?   (浏览器插件)
	* 一位华裔前Google工程师开发的前端js库
    * 与angular.js类似的是声明式开发，但性能高于angular，体积小很多, 比较适合移动端开发
    * 它本身不是全能框架, 只关注UI, 如果需要router/ajax, 可以使用对应插件或使用别的库来实现
  
  * 响应的数据绑定：通常页面的数据(Model)变化需要操作DOM，改变html(View)页面，
    Vue直接绑定DOM，数据(Model)变HTML(View)变，不用操作DOM
  * 组件系统：自定义元素
    
* 基本使用
	* 引入vue.js  
	  - 1.<script> 标签引入，Vue会被注册为一个全局变量(构造函数)
	  - 2.大型框架推荐使用 NPM 安装 npm install vue
	      - 快速搭建大型单页应用 vue-cli        
           npm install -g vue-cli     全局安装 vue-cli       
           vue init webpack my-project  创建一个基于 "webpack" 模板的新项目  
           cd my-project
           npm install    安装依赖，走你
           npm run dev  
            
* Vue对象的选项,Vue为构造函数，new Vue（）创建一个实例对象 		
  * this使用:Vue对象中定义的data，methods，computed均是其对象或属性，可以直接this调用         
	* 创建Vue对象,Vue中的-对象方法-在View可以直接用                                -- VM --
		* el : 指定dom标签容器的选择器,注意（#,.,元素）   -- view --
		* data : 指定初始化状态属性数据的对象            -- model --
		        对象
		        函数(返回一个对象)
		* methods:事件指令的回调函数,data中数据可以直接this.xxx调用
		        对象  属性值为函数
		        事件 @click='myClick()',括号内可传形参，调用时用。
		            v-on:click='myClick()'
		* computed:计算属性,白话为了方便data中数据的计算,可以动态的随着data中数据变化而变化  
		        对象  属性值为函数 
		        常用 set 和 get方法  
		* watch:监视属性                       
		            
？？？？？？？？？？？？？
* $event对应的是原生DOM的属性，相当于浏览器调用时的回调函数，target		            		            
* 为了方便我们在事件回调函数中存取 View 层的数据，Vue.js 在事件对象上增加了一个叫做 targetVM 的属性，	            
？？？？？？？？？？？？？？？？？？？		            
		          	            
    * el
      * 指定dom标签容器的选择器
      * Vue就会管理对应的标签及其子标签
    * data
      * 指定初始化状态属性数据的对象
      * vue对象可以直接访问其属性
      * 页面中可以直接访问使用
    * methods
      * 包含多个方法的对象
      * 供页面中的事件指令来绑定回调
      * 回调函数默认有event参数, 但也可以指定自己的参数
      * 所有的方法由vue对象来调用, 访问data中的属性直接使用this.xxx
    * computed 
      * 包含多个方法的对象
      * 对状态属性进行计算返回一个新的数据, 供页面获取显示
      * 一般情况下是相当于是一个只读的属性
      * 利用set/get方法来实现属性数据的计算读取, 同时监视属性数据的变化
    * watch
      * 包含多个属性监视的对象
      * 分为一般监视和深度监视
      * 'xxx' : {
        deep : true,
        handler : fun(vlaue)
      }

* 页面指令-表达式: 数据解析{{}}以及页面指令的值都是表达式
	* 使用v-model: 实现双向数据绑定,括号内text,html均为表达式
	* 使用{{text}}===v-text="text" ; 显示数据text，单向数据传递，从data传向View 
	* 使用{{{html}}}===v-html="html" ; 显示数据html，单向数据传递，从data传向View
	  - 引出强制数据绑定比如<a href='{{url}}'></a>  或<a v-bind:href='url'></a> 
		
* 解决闪退问题      
  * v-cloak 样式: [v-cloak] { display: none } 配合使用,写在父标签上    
	* v-text/v-html: 指定标签体 
		* v-text : 当作纯文本   =>{{}}
		* v-html : 将value作为html标签来解析  =>{{{}}}
		
* 强制绑定：绑定事件 or 数据强制绑定	
	* v-on : 绑定事件监视
		* v-on:事件名, 可以缩写为: @事件名
		* 监视具体的按键: @keyup.keyCode   @keyup.enter
		* 阻止事件的冒泡和事件默认行为: @click.stop   @click.prevent
		* 隐含对象: $event
	* v-bind :(:id='nanme'),强制绑定解析表达式,把属性值看成表达式,class和style	  
		* 很多属性值是不支持表达式的, 就可以使用v-bind
		(补充：vue)
		* :class  名称不能有大写
			* :class="{classA : isA, classB : isB}"
			* :class="[classA, classB]"
		* :style
			:style="{color : color}"		
		  理解：正常情况下 class='myclass',class对应的是字符串
				在Vue中，静态class和普通写法一样
				动态写法几种常见方法 （）
				1. class = {{myclass}}  myclass是表达式 data  myclass="myclass"
				2.强制绑定写法
				 1.对象写法 :class='{myclass：bullun}'
				 2.数组写法（js语法） :calss="['myclass']"或:calss="[myclass]" data myclass='myclass' 

	* v-el : 标识某个标签
		* v-el:xxx
		* 读取得到标签对象: this.$els.xxx

	* v-if v-else v-show
	  - v-if直接不渲染这个DOM元素，而v-show是会渲染DOM元素，只是使用display:none隐藏，
		* v-if : 如果vlaue为true, 当前标签会输出在页面中,
		  - template：渲染多个元素
		* v-else : 与v-if一起使用, 如果value为false, 将当前标签输出到页面中
		* v-show: 就会在标签中添加display样式, 如果vlaue为true, display=block, 否则是none
		
	* v-for : 遍历，写在子标签上
		* 遍历数组 : v-for="person in persons"   $index
		* 遍历对象 : v-for="value in person"   $key		
		- 删除方法：1.根据下标index,splice(index,1)
		           2.过滤器影响数组排序，根据数组对象删除
		           index = this.persons.indexOf(item)
		           splice(index,1)
		           3.新属性 $remove(item) : 删除数组中对应的元素
		
		
* 过滤器
    * 内置
        1. capitalize : 首字母大小e
        2. uppercase : 全部大写
        3. lowercase : 全部小写
        4. currency : 货币化
        5. pluralize : 单数/复数处理
        6. json : json格式化
        7. limitBy : 限定数组的部分元素(下标)
        8. filterBy : 限定数组的部分元素(值)
        9. orderBy : 对数组进行排序
    * 自定义
        1. 全局过滤器
            Vue.filter('过滤器名', function(value, xxx, yyy) {
                //处理逻辑
                return result;
            });
        2. 局部过滤器
            new Vue({
                filters : {
                    '过滤器名' : function(value, xxx, yyy) {
                        //处理逻辑
                        return result;
                    }
                }
            })
* 指令
    * 内置
        v:text : 更新元素的 textContent
        v-html : 更新元素的 innerHTML
        v-if : 如果为true, 当前标签才会输出到页面
        v-else: 如果为false, 当前标签才会输出到页面
        v-show : 通过控制display样式来控制显示/隐藏
        v-for : 遍历数组/对象
        v-on : 绑定事件监听, 一般简写为@
        v-bind : 强制绑定解析表达式, 可以省略v-bind
        v-model : 双向数据绑定
        v-el : 为某个元素注册一个唯一标识, vue对象通过$els属性访问这个元素对象
        v-cloak : 使用它防止闪现表达式, 与css配合: [v-cloak] { display: none }
    * 自定义
        1. 注册全局指令
            Vue.directive('my-directive', function(value){
                this.el.innerHTML = value.toUpperCase();
            })
        2. 注册局部指令
            directives : {
                'my-directive' : function(value) {
                    this.el.innerHTML = value;
                }
            }
        3. 使用指令:
            v-my-directive='xxx'
* 扩展数组
	* $remove(item) : 删除数组中对应的元素
	* $set(index, ele) : 给数组中指定下标指定对应的元素  
	           
* 组件:组件可以扩展HTML元素,封装可重用的代码.在较高层面上,组件是自定义元素,Vue.js的编译器为它添加特殊功能
  * 不需要全局注册每个组件。可以让组件只能用在其它组件内，用实例选项 components 注册

* todoList练习


## npm与package.json
* npm
  * 全称: Node Package Manager
  * node服务器端与前端通用的基于命令的包管理工具
  * 包?: 可以简单的理解就是一个应用/库(具有特定功能)
  * 包管理器: 对当前应用依赖的其它包进行下载及管理的工具(包)
  * npm常用命令:
    * npm init
    * npm install
    * npm install packageName --save
    * npm install packageName@version --save
    * npm install packageName --save-dev
    * npm install packageName -g
    * npm info packageName
    * npm rm packageName
* package.json
  * 当前应用包的相关描述信息, 是一个json对象
  * 重要信息:
    * name: 当前包名
    * version: 当前包版本号
    * scripts: n个可执行的命令
    * dependencies: n个运行依赖的包
    * devDependencies: n个开发编译依赖的包