# 测试State

setState是异步的，所以:

```
this.setState({foo: 'bar'});
console.log(this.state.foo);
```
会得不到预期的数值。

解决的办法是用回调函数。

```
this.setState({value: event.target.value}, function () {
    console.log(this.state.value);
});
```

### 参考
http://stackoverflow.com/questions/30782948/why-calling-react-setstate-method-doesnt-mutate-the-state-immediately