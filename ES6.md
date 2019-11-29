# ES6-
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
            如果只有一个参数，圆括号可选的，可以用也可以不用。
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
      set它类似于数组，但是成员的值都是唯一的，没有重复的值。Set本身是一个构造函数，用来生成 Set 数据结构。
      Set 结构的实例有以下属性：
              Set.prototype.constructor：构造函数，默认就是Set函数。
              Set.prototype.size：返回Set实例的成员总数。
      set有两大类，操作方法（用于操作数据）和遍历方法（用于遍历成员）。
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
       
       




  
  




