# ES6-
ES6学习笔记

基本用法
一：变量
es6声明变量的6中方法：var   function    let      const   import   class 。
let和const的相同部分：
  1：存在块级作用域；
  2：不存在变量提升，但var会提升；
  3：暂时性死区；
  4：不允许重复声明。
  
const: 特性跟let一样，const定义变量不能修改，且定义的时候必须有值，不能后赋值，不能修改。
如果不修改变量，使用const。let适合for循环。
for循环的变量i跟函数内部的变量i不在同一作用域内，有各自单独的作用域。
例子：for (let i = 0; i < 3; i++) {
        let i = 'abc';
        console.log(i);
    }
  // abc
  // abc
  // abc

二：暂时性死区
暂时性死区就是所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
但也意味着typeof不是百分百的操作，没有let之前typeof是百分百安全的，永远不会报错。





  
  




