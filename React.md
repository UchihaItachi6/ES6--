REACT 学习笔记

一：

一：es6的写法
  class Counter extends React.Component {   // 创建一个Counter的组件
    constructor(props) {   //props 是属性，也可以理解为参数
    super(props);    
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
  ReactDOM.rendr(<Counter/>,document.getElementById('id'));  //第一个是组件，第2个是DOM节点
