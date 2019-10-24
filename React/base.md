### 关键点
1. 向事件处理程序传递参数

``` javascript
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

2. 回调函数this处理

``` javascript
// 1. 箭头函数
  handleClick = () => {
    console.log('this is:', this);
  }

// 2. 构造器中绑定
 constructor(props) {
    super(props);
    this.state = {};
    // This binding is necessary to make `this` work in the callback
    // 事件处理函数绑定this
    this.handleClick = this.handleClick.bind(this);
  }

// 3. 事件监听处绑定this
 <button onClick={(e) => this.handleClick(e)}>
```

3. 手动双向绑定
> 监听表单变化，更新组件状态
```javascript
 handleChange(event) {
    this.setState({value: event.target.value});
  }
<input type="text" value={this.state.value} onChange={this.handleChange} />
```
4. 子父通信
> react 调用父组件提供的方法修改props

> vue bus事件通知父组件，父组件中修改

> 共同点：修改props在父组件内进行，子组件不进行直接操作

> 如果某些数据可以由props或者state提供，那么它很有可能不应该在state中出现

5. 子组件

5.1. 调用父组件，将子组件传入，父组件渲染
``` javascript
// 调用FancyBorder组件，传入要渲染的子组件
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
// 以props.children的形式接受子组件并渲染
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```

```javascript
// 子组件有多个，从props中提取并渲染
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}
// 调用时按属性传入传入子组件
function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```
5.2  根据props传入的值，渲染对应的组件（可能值和需要渲染的组件一一对应）

6. 组件复用

> 通过传入的props复用组件（子组件也可通过props传入）

> React 具有强大的组合模型，我们建议使用组合而不是继承来复用组件之间的代码。

> 如果要在组件之间复用 UI 无关的功能，我们建议将其提取到单独的 JavaScript 模块中。这样可以在不对组件进行扩展的前提下导入并使用该函数、对象或类。

7. for循环

```javascript
 {(function() {
          let a = [];
          for (let item of [1, 2, 3]) {
            a.push(<div> {item} </div>);
          }
          return a;
   })()}
```

8. 嵌套路由 子路由与子组件在父组件定义与引入

```jsx
<section className="waterQuality-list">
        <Route path="/nantong/peoplelivelihood/waterqualitylist/:waterQualityId" component={WaterQualityDetail} />
        <div className="list-item">
          <div className="list">
            <ListView
              key={'1'}
              dataSource={dataSource}
              renderRow={row}
              renderSeparator={separator}
              useBodyScroll={this.state.useBodyScroll}
              style={this.state.useBodyScroll ? {} : { height: this.state.height }}
              pullToRefresh={<PullToRefresh
                refreshing={refreshing}
                onRefresh={this.onRefresh}
              />}
              onEndReached={this.onEndReached}
              onEndReachedThreshold={120}
              pageSize={waterQualityList.length}
            />
          </div>
          <Footer />
        </div>
      </section>
```



8. 子组件数据可以存储在父组件中