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
   let [head,..tail] = [1,2,3,4];
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
      
      
         
  
      
   
   
   
   
  
   
   






  
  




