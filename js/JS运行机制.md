### JS运行机制

1. 进程、线程

   - 进程是相互独立的

   - 一个进程可以由一个或者多个线程组成

   - 多个线程在进程中协作完成任务

   - 同个进程下的各个线程直接共享程序的内存空间

2. 进程是cpu资源分配的最小的单位  线程是cpu调度的最小单位
3.  所谓的单线程多线程，是指在一个进程内的单个和多个，核心还是属于一个进程的
4.  浏览器是多进程的
	- Browser进程：浏览器的主进程（负责协调、主控），只有一个。
	- 第三方插件进程：每种类型的插件对应一个进程，仅当使用该插件时才创建
	- GPU进程：最多一个，用于3D绘制等
	- 浏览器渲染进程（浏览器内核）（Renderer进程，内部是多线程的）：默认每个Tab页面一个进程，互不影响。
	
5. 常驻线程
	1. GUI渲染线程
		- 负责渲染浏览器界面，解析HTML，CSS，构建DOM树和RenderObject树，布局和绘制等。
		- 当界面需要重绘（Repaint）或由于某种操作引发回流(reflow)时，该线程就会执行
		- 注意，__GUI渲染线程与JS引擎线程是互斥的__，当JS引擎执行时GUI线程会被挂起（相当于被冻结了），__GUI更新会被保存在一个队列中等到JS引擎空闲时立即被执行__。
	
	2. JS引擎线程
		- 也称为JS内核，负责处理Javascript脚本程序。（例如V8引擎）
		- JS引擎一直等待着任务队列中任务的到来，然后加以处理，一个Tab页（renderer进程）中无论什么时候都只有一个JS线程在运行JS程序
		- 同样注意，__GUI渲染线程与JS引擎线程是互斥的__，所以如果JS执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞。
	
	3. 事件触发现场
		- 归属于浏览器，用来控制时间循环
		- 当JS引擎执行代码块如setTimeOut时（也可来自浏览器内核的其他线程,如鼠标点击、AJAX异步请求等），会将对应任务添加到事件线程中
		- 当对应的事件符合触发条件被触发时，该线程会把事件添加到待处理队列的队尾，等待JS引擎的处理
		- 注意，由于JS的单线程关系，所以这些待处理队列中的事件都得排队等待JS引擎处理（当JS引擎空闲时才会去执行）
	
	4. 定时触发器线程
		- 传说中的setInterval与setTimeout所在线程
		- 浏览器定时计数器并不是由JavaScript引擎计数的,（因为JavaScript引擎是单线程的, 如果处于阻塞线程状态就会影响记计时的准确）
		- 因此通过单独线程来计时并触发定时（计时完毕后，添加到事件队列中，等待JS引擎空闲后执行）
		- 注意，W3C在HTML标准中规定，规定要求setTimeout中低于4ms的时间间隔算为4ms。
      
      5. 异步http请求线程
      	 - 在XMLHttpRequest在连接后是通过浏览器新开一个线程请求
      	 - 将检测到状态变更时，如果设置有回调函数，异步线程就__产生状态变更事件__，将这个回调再放入事件队列中。再由JavaScript引擎执行。

6. SharedWorker由独立的进程管理，WebWorker只是属于render进程下的一个线程
7. 复合图层：GPU中，各个复合图层是单独绘制的，所以互不影响  __Chrome源码调试 -> More Tools -> Rendering -> Layer borders中看到，黄色的就是复合图层信息 __


