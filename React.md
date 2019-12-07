REACT 学习笔记
1111
 一： react的安装 ，如果没有类似umi的框架的话就要引入3个库:
        react.min.js - React 的核心库
        react-dom.min.js - 提供与 DOM 相关的功能
        babel.min.js - Babel 可以将 ES6 代码转为 ES5 代码
       div 中的所有内容都将由 React DOM 来管理，所以我们将其称为 "根" DOM 节点。
      react的导入:
	import React from 'react' 只导入 是 React。
	而 import * as React from 'react' 导出所有，并命名为 React。
	而 import hash as Router from 'react' 导出hash，并命名为 Router。
      关于React注释的问题：
        1、在标签内部的注释需要花括号                 
        2、在标签外的的注释不能使用花括号
           ReactDOM.render(
              /*注释 */
              <h1>孙朝阳 {/*注释*/}</h1>,
          document.getElementById('example')
         );
         
 二： React JSX   
    优点和注意事项：（1）JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
                   (2) 它是类型安全的，在编译过程中就能发现错误。
                   (3) 使用 JSX 编写模板更加简单快速。
                   (4)在添加属性时， class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。
                   (5)使用jsx的地方，script里都要加入 type="text/babel"
                   (6)遇到{}解析的是JS的语法，遇到<>解析的是html的语言,组件里是不能写style样式.
                   (7)注意style属性要用驼峰命名法表示，如: backgroundColor 而不是 background-color，fontSize 而不是 font-size
             
三：React组件    
     function HelloMessage(props) {
          return <h1>Hello {props.name}!</h1>;
      }
      const element = <HelloMessage name="Runoob"/>;  // name="Runoob" 这个就是props    
      ReactDOM.render(
         element,
         document.getElementById('example')
      );
      
   es6的写法
    class Counter extends React.Component {   // 创建一个Counter的组件   extends实现类的继承
      // constructor 是一个构造方法，也是一个函数，如果没有定义会自动添加   
      constructor(props) {   //构造方法一个类只能有一个constructor        props 是属性，也可以理解为参数  
      super(props);       //super也就是继承要在this之前   我的理解就是等于 var _this = this， 用来初始化this
        this.state = {
          count: 0// 初始化数据
        }
        this.increment = this.increment.bind(this);  //将下面函数的this绑定在一起
        this.decrement = this.decrement.bind(this);
        this.reset = this.reset.bind(this);
      }
      increment(){
        this.setState({  count: this.state.count + 1 });  // this。state   重新渲染数据
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
    ReactDOM.rendr(<Counter/>,document.getElementById('id'));
  
   ReactDOM.render()是渲染方法，第一个参数是组件的显示，第2个是渲染的地方
   unmountComponentAtNode() 这个方法是解除渲染挂载，作用和 render 刚好相反，也就清空一个渲染目标中的 React 部件或 html 内容。
   可以通过this.props来访问props，但不能修改它。一个组件绝对不能修改自己的props。
   state 和 props 主要的区别在于 props 是不可变的，而 state 可以根据与用户交互来改变。这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。
   props可以把任意类型的数据传递给组件,通过this.props.来访问.但是不能修改它,一个组件绝对不能修改自己的props.
   constructor 可以理解为纯函数，render函数应该也为纯函数。
   原生的HTML元素以小写字母开头，自定义React组件开头名字要大写 ，组件里面只能包含一个顶层标签。   
   所有组件都必须有一个render的方法，用于输出组件。
   
四：组件的生命周期
   什么是生命周期函数？  生命周期函数（钩子函数）通俗的说就是在某一时刻会被自动调用执行的函数。
   组件的生命周期分成三个状态： 
				(1)Mounting：已插入真实 DOM
				(2)Updating：正在被重新渲染
				(3)Unmounting：已移出真实 DOM
   
  React 为每个状态都提供了两种处理函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用，三种状态共计五种处理函数。  		
    				componentWillMount();
				componentDidMount();
				componentWillUpdate(object nextProps, object nextState);
				componentDidUpdate(object prevProps, object prevState);
				componentWillUnmount() ;


 （1）挂载（Mounting）：	
  componentWillMount是在render前，所以setState不会重新渲染。
  注意：改生命周期在未来17版本中将被弃用(在这里请求异步数据，render可能不会渲染到，因为componentWillMount执行后，render立马执行)
  组件被挂载到页面之前调用，整个生命周期中只会调用一次（组件更新时不会再调用）。 注意：在这里可修改state

 （2）	
  componentDidMount是在render后，调用setState会重新渲染，页面可交互，可以请求数据.组件被挂载到页面之后调用，整个生命周期只调用一次（组件更新不会调用）。
  建议：在这里可以异步请求数据。在这里设置状态会触发重新渲染。但是不推荐在这里使用setState函数，它会触发一次额外的渲染，而且是在浏览器刷新屏幕之前执行，用户看不到这个状态。在这里使用setState函数会导致性能问题。

  更新（Updating）：
  componentWillUpdate(nextprops,nextstate)；  注意：此生命周期在未来17版本中将被弃用。
  组件更新之前（componentshouldupdate返回true）时调用，组件初始化时不调用
  注意：在这里可以更改state，nextstate.xxx = xxx,但是在这里不能调用setState函数，这会导致函数调用componentshouldupdate从而进入死循环。

 componentDidUpdate()； 组件更新完成之后调用，组件初始化时候不调用。注意：可以在这里获取dom。

  
	

  
 
