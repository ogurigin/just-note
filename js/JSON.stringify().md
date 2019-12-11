###  JSON.stringify()
#### 九大特性
1. - undefined、任意的函数、symbol最为对象的属性值的时候，JSON.stringify()将跳过对他们的序列化
	- 三者作为数组的元素的时候，SON.stringify()会将他们序列化成 null
	- 三者作为单独的值时，会被序列化成 undefined。
2. 因为的一个特性的关系，导致非数组对象的属性不一定以特定的顺序出现。
3. 转换的值中如果有 toJSON() 函数的话，该函数的返回值就是序列化的结果，并且会忽略掉其他的属性值。
4. 因为date对象自己部署了 toJSON()方法，因此date 对象会被当成字符串处理
` eg：JSON.stringify({ now: **new** Date() });
// "{"now":"2019-12-08T07:42:11.973Z"}" `
5. NAN 、Indinity 格式的数值 以及 null 都会被当成null
6. 布尔值，数字，字符串的包装对象 在序列化过程中会被自动转换成对应的原始值
   `  JSON.stringify([new Number(1), new String("false"), new Boolean(false)]);
    	// "[1,"false",false]"` 
 7. 其他类型的对象，包括 Map/Set/WeakMap/WeakSet，仅会序列化可枚举的属性。
 8. 利用JSON.parse(JSON.stringify()) 实现深拷贝的时候，遇到包换循环引用的对象（对象之间相互引用，形成无限循环）时，会抛出错误
 9. 以symbol为属性键的属性都会被完全忽略掉，即便 ***replacer***参数中强制指定了包含他们



### 关于第二个参数replacer

​	replacer 是 JSON.stringify()的第二个参数。他可以是一个函数或者一个数组。

1. 当replacer是个 数组的时候，数组的值就代表将被序列化的属性名。

2. 当replacer是个函数的时候，可以打破九大特性的大多数特性

   - **replacer 被传入的函数时，第一个参数不是对象的第一个键值对，而是空字符串作为 key 值，value 值是整个对象的键值对**

     `const data = {  a: 2,  b: 3,  c: 4,  d: 5 };`

      `JSON.stringify(data, (key, value) => {` 

      `console.log(value);  return value; })` 

     `// 第一个被传入 replacer 函数的是 {"":{a: 2, b: 3, c: 4, d: 5}}`

   ### 关于第三个参数
   
   	1. 果然是个数字，则在字符串化时每一级别会比上一级别缩进多这个数字值的空格（最多10个空格）；
    	2. 如果是一个字符串，则每一级别会比上一级别多缩进该字符串（或该字符串的前10个字符）。

