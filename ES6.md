﻿# ES6-
ES6学习笔记

基本用法
一：变量
变量一定要先声明在使用
es6声明变量的6中方法：var   let    const    import   class  function 。
let和const的相同部分：
  1：存在块级作用域；
  2：不存在变量提升，但var会提升；
  3：暂时性死区；
  4：不允许重复声明。
  
const: 特性跟let一样，const定义变量不能修改，且定义的时候必须有值，不能后赋值，不能修改。
但是可以添加新属性。let可以不赋值，并且let的值可以修改

如果不修改变量，使用const。let适合for循环。
for循环的变量i跟函数内部的变量i不在同一作用域内，有各自单独的作用域。
例子：for (let i = 0; i < 3; i++) {
        let i = 'abc';
        console.log(i);
    }
  // abc
  // abc
  // abc
  
暂时性死区:
  暂时性死区就是所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
  但也意味着typeof不是百分百的操作，没有let之前typeof是百分百安全的，永远不会报错。
  es6块级作用域必须有大括号，没有的话js引擎就认为不存在块级作用域。
  

二：变量的解析赋值
   let [head,...tail] = [1,2,3,4];
   console.log(head)   //  1
   consloe.log(tail)   //2,3,4
   如果解构不成功，变量的值就等于undefined。如果右边的等号不是数组的话也会报错。
    let [foo] = 1;
    let [foo] = false;
    let [foo] = NaN;
    let [foo] = undefined;
    let [foo] = null;
    let [foo] = {}；
   以上几个都会报错。
   
   解构赋值允许指定默认值。
   let [foo = true] = [];   foo // true
   如果值为空或者为undefind的时候，默认值才会生效。就算值为null，默认值也不会生效。值为null
   let [x = 1] = [undefined];
    x // 1
   let [x = 1] = [null];
    x // null
   
三：对象的解构赋值
      解析不仅可以用于数组还可以用于对象。
      对象跟数组解构赋值的不同：
        数组是按照元素的顺序排列的，变量的值取决它的位置。
        对象的属性没有顺序，是根据相同的模式来找值的，相同模式下的value赋值给key；
        let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
        foo为匹配的模式，baz才是变量（key），找到相同模式以后，将后面的vlaue赋值给key。
      对象的解构也是可以指定默认值的。
        var {x : y=3} = {x:5};   //y=5;   x为模式，y为默认值。
        跟数组的解构赋值一样，没有值和为undefind的时候才会为默认值。
        
        
四：函数参数的解构函数
      函数参数的解构也可以使用默认值。
       function move({x = 0, y = 0} = {}) {
          return [x, y];
        }
          move({x: 3, y: 8}); // [3, 8]
          move({x: 3}); // [3, 0]
          move({}); // [0, 0]
          move(); // [0, 0]     
  
  五：圆括号问题
        es6可能导致解构的歧义，就不得使用圆括号也是小括号，能不用就不用。
        可以使用小括号的情况只有一种：赋值语句的非模式部分，可以使用小括号。
        
  六：解构赋值的用途
     （1）交换变量的值              以前的交换变量
          let x = 1；                  var t;
          let y = 2;                   t=a;
          [x,y] = [y,x];               a=b, b=t;
     （2）从函数返回多个值
          const people = {
            name:'yu',                  
            age:'24',                   
          }                             ------>
          const name = people.name;         
          const age = people.age;       ------>     const { name,age } = people;
          
  七：字符串的扩展    
        模板字符串用反引号标识。
        所有模板字符串的空格和换行，都是被保留的，比如<ul>标签前面会有一个换行。如果你不想要这个换行，可以使用trim方法消除它。
        字符串中嵌入变量，需要将变量名写在${}之中。
         let name = "Bob", time = "today";
         `Hello ${name}, how are you ${time}?`  // Hello Bob,how are you today?
         模板字符串还能调用函数
          function fn(){
            return "Hello Word",
          }
          `foo ${fn()} bar`   //foo Hello World bar
        标签模板：
        模板字符串可以跟一个函数在后面，标签模板其实不是模板，而是函数调用的一种特殊形式。“标签”指的就是函数，紧跟在后面的模板字符串就是它的参数
        tag(['Hello ', ' world ', ''], 15, 50)
      
   八：数值的扩展
        Number.parseInt === parseInt // true                parseInt() 函数可解析一个字符串，并返回一个整数。
        Number.parseFloat === parseFloat // true            parseFloat() 函数可解析一个字符串，并返回一个浮点数。
        Number.isInteger()用来判断一个数值是否为整数。
        Math.trunc()方法用于去除一个数的小数部分，返回整数部分
        Math.sign()方法用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值。
        它会返回五种值：
                      参数为正数，返回+1；       Math.sign(5) // +1
                      参数为负数，返回-1；       Math.sign(-5) // -1
                      参数为 0，返回0；          Math.sign(0) // +0
                      参数为-0，返回-0;          Math.sign(-0) // -0
                      其他值，返回NaN。          Math.sign(NaN) // NaN
  
 九：函数的扩展
        res参数（形式为...变量名），rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。
        函数的length属性，不包括 rest 参数。     
            (function(a) {}).length  // 1
            (function(...a) {}).length  // 0
            (function(a, ...b) {}).length  // 1
        严格模式 --- 'use strict';规定只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。
        箭头函数：
            如果箭头函数不需要参数或需要多个参数，就使用一个圆括号代表参数部分。function省略了。
            当你的函数有且仅有一个参数的时候，是可以省略掉括号的；当你函数中有且仅有一个表达式的时候可以省略{}
                 箭头函数有几个使用注意点：
                （1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
                （2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
                （3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
                （4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。
                上面四点中，第一点尤其值得注意。this对象的指向是可变的，但是在箭头函数中，它是固定的。

十： 数组的扩展
      扩展运算符（spread）是三个点（...）.
      
十一 ： 对象的扩展     
        属性名的简洁表示法 : ES6允许在代码中直接写变量，变量名是属性名，变量值是属性值。
          let key = "value";
          let obj = {key};//obj {key : "value"}
        对象的name属性：对象里的方法的name属性返回方法所对应的方法名
        如果是对象里的get方法或者set方法，则对象方法的name属性返回get/set 函数名
              let cat = {
                     age:1,
                     set mini(a){
                       this.age = age;
                     }s
                     get mini(){
                       return this.age;
                     }
                  }
              cat.mini.name //undefined
              Object.getOwnPropertyDescriptor(cat,'mini').get.name //'get mini'
              Object.getOwnPropertyDescriptor(cat,'mini').set.name//'set mini'
        bind方法创造的对象的函数，name属性返回的是"bound" 方法名
                      let obj = {
                          test(){}
                      }s
                      obj.test.bind().name //"bound test"
十二：Set 和Map
      ES6有4种数据集合：数组（array），对象（object）,set,map.
      Set它类似于数组，但是成员的值都是唯一的，没有重复的值。Set本身是一个构造函数，用来生成 Set 数据结构。
      Set 结构的实例有以下属性：
              Set.prototype.constructor：构造函数，默认就是Set函数。
              Set.prototype.size：返回Set实例的成员总数。
      Set有两大类，操作方法（用于操作数据）和遍历方法（用于遍历成员）。
            操作数据：
              Set.prototype.add(value)：添加某个值，返回 Set 结构本身。
              Set.prototype.delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
              Set.prototype.has(value)：返回一个布尔值，表示该值是否为Set的成员。
              Set.prototype.clear()：清除所有成员，没有返回值。
            遍历成员：
              Set.prototype.keys()：返回键名的遍历器
              Set.prototype.values()：返回键值的遍历器
              Set.prototype.entries()：返回键值对的遍历器
              Set.prototype.forEach()：使用回调函数遍历每个成员
       Map语法： new Map([iterable])  Iterable 可以是一个数组或者其他 iterable 对象，其元素为键值对(两个元素的数组，例如: [[ 1, 'one' ],[ 2, 'two' ]])。 每个键值对都会添加到新的 Map。null 会被当做 undefined。
       （1）一个Object的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值，包括函数、对象、基本类型。
       （2）Map 中的键值是有序的，而添加到对象中的键则不是。因此，当对它进行遍历时，Map 对象是按插入的顺序返回键值。
       （3）Map 的键值对个数可以从 size 属性获取，而 Object 的键值对个数只能手动计算。
       （4）Object 都有自己的原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。
       
十三：Iterator 和 for...of 循环
      Iterator(遍历器),Iterator 接口主要供for...of消费。
      terator 的遍历过程是这样的。
     （1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。
     （2）第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。
     （3）第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。
     （4）不断调用指针对象的next方法，直到它指向数据结构的结束位置。
      Symbol.iterator 方法创建一个迭代器，之后不断的调用 next 方法对数组内部项进行访问
      我的理解就是你要访问里面的value，必须要用next的方法才能访问到。next的方法会返回两个属性value和done
      value属性是当前成员的值，done属性是一个布尔值，表示遍历是否结束。done为false说明没有结束，为true的时候才结束
      以下是可迭代的值:Array，String，Map，Set，Dom元素（正在进行中）。都是用for..of循环
十四：Generator 函数的语法
      Generator（生成器）函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield表达式，定义不同       的内部状态（yield在英语里的意思就是“产出”）。但是如果要用yield的话必须满足两个条件：必须是生成器函数，必须要用.next的方法。
      生成器函数不会像其他函数一样立即执行，而是返回一个指向内部状态对象的指针，所以要调用遍历器对象Iterator 的 next 方法，指针就会从函数头部或者上      一次停下来的地方开始执行。
      写法： function* 函数名(x,y){ ...}  访问里面的值 ----函数名.next（）
      Generator里的return方法 ，可以返回固定的值，并且结束生成器函数。如果return方法调用时，不提供参数，则返回值的value属性为undefined。
            function* foo(){
                  yield 1;
                  yield 2;
                  yield 3;
              }
        var f = foo();
        f.next();
        // {value: 1, done: false}
        f.return("foo");
        // {value: "foo", done: true}
        f.next();
        // {value: undefined, done: true}
        yield* 表达式表示 yield 返回一个遍历器对象，用于在 Generator 函数内部，调用另一个 Generator 函数。
十五： CLASS类
      可以通过class关键字定义类，class的本质是function。类表达式可以为匿名或者命名，但是不能重复。
      类不会被提升，也不会有function的关键字，方法间不能加分号。
      constructor方法是类的默认方法，创建类的实例化被调用。实例化必须要用new关键字。
      
      
        
   
      
      
  




