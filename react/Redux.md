### Redux

#### 三大原则：

1. 单一数据源：

   整个应用的state被储存在一棵object tree 中，并且这个objuct tree 只存在唯一一个的store中。

2. state是只读的

   唯一改变state的方法是出发action，action是一个用于描述已发生事件的普通对象。

3. 使用纯函数来执行修改

   为了描述action如何改变state tree ，需要编写reducers。

   reducer是纯函数，接收之前的state和action，然后返回新的state。



#### Action

1. action 是把数据从应用层传递到store的有效载体，**是store数据的唯一来源**
2. 本质上就是js的普通对象
3. 必须使用一个字符串格式类型的type字段来表示将要执行的动作
4. 是为了表示 某个对象发生了什么行为，尽量减少action中传递的数据



#### reducer

1. reducer是个纯函数，接受当前的state和action，返回新的state
2. 传入的参数相同的情况下，返回的newstate一定相同。
3. 保持reducer纯净是非常主要的，**不要在reducer中做这些操作：** 
   - 修改传入的参数
   - 执行有副作用的操作：eg APi请求和路由跳转
   - 调用非纯函数，如 Date.now()或Mate.random();
4. 不要修改previousState的值，创建一个新的对象返回给newSate。



#### store

1. 一个redux应用只有一个store，store保证了唯一的数据源

2. store的职责：

   - 持有应用的state

   - 提供getState()方法获取state

   - 提供dispatch()方法更新state

   - 用过subscribe（listener）注册监听器

   - 通过subscribe（listener）返回的函数注销监听器

     

#### redux数据流

生命周期：

1. 调用store.dispatch(action)发送Action
2. redux根据传入的action调用对应的reducer方法
3. 根据reducer把 子reducer的结果合成一棵state树
4. redux store保存根reducer生成的state树



