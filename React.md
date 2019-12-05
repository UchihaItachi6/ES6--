REACT 学习笔记

一：es6的写法
  class Counter extends React.Component {   // 创建一个Counter的组件   extends实现类的继承
    constructor(props) {   //props 是属性，也可以理解为参数  
    super(props);       //super必须出现在this之前   我的理解就是等于 var _this = this;
      this.state = {
        count: 0// 初始化数据
      }
      this.increment = this.increment.bind(this);  //将下面函数的this绑定在一起
      this.decrement = this.decrement.bind(this);
      this.reset = this.reset.bind(this);
    }
    increment(){
      this.setState({  count: this.state.count + 1 });  //重新渲染数据
    }
    decrement(){
      this.setState({   count: this.state.count - 1 });
    }
    reset(){
      this.setState({   count: 0 });
    }
    render(){
      return(
        <div>       //最外层只能有一个标签，不一定是div，可以是组件
          <Test/>   //里面可以有多个标签跟组件
          <App/>
          <button className='inc' onClick={this.increment}>Increment!</button>
          <button className='dec' onClick={this.decrement}>Decrement!</button>
          <button className='reset' onClick={this.reset}>Reset</button>
          <h1>Current Count: {this.state.count}</h1>
        </div>
      );
    }
  }
  ReactDOM.rendr(<Counter/>,document.getElementById('id'));   //ReactDOM.render()是渲染方法，第一个参数是组件的显示，第2个是渲染方法
  // unmountComponentAtNode() 这个方法是解除渲染挂载，作用和 render 刚好相反，也就清空一个渲染目标中的 React 部件或 html 内容。

  二： react的安装 ，如果没有类似umi的框架的话就要引入3个库:
        react.min.js - React 的核心库
        react-dom.min.js - 提供与 DOM 相关的功能
        babel.min.js - Babel 可以将 ES6 代码转为 ES5 代码
       div 中的所有内容都将由 React DOM 来管理，所以我们将其称为 "根" DOM 节点。
      关于React注释的问题：
        1、在标签内部的注释需要花括号                 
        2、在标签外的的注释不能使用花括号
           ReactDOM.render(
              /*注释 */
              <h1>孙朝阳 {/*注释*/}</h1>,
          document.getElementById('example')
         );
         
  React JSX   
      优点： （1）JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
             (2) 它是类型安全的，在编译过程中就能发现错误。
             (3) 使用 JSX 编写模板更加简单快速。
             
三：React组件    
      原生的HTML元素以小写字母开头，自定义React组件开头名字要大写 ，组件里面只能包含一个顶层标签。   
      function HelloMessage(props) {
          return <h1>Hello {props.name}!</h1>;
      }
      const element = <HelloMessage name="Runoob"/>;  // name="Runoob" 这个就是props    
      ReactDOM.render(
         element,
         document.getElementById('example')
      );
      在添加属性时， class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。
      
     


  
 
