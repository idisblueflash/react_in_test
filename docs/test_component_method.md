# 测试React组件的method

比如我们想测试TextInput失去焦点后，调用handleCheckPhoneNumber的method。

这里用sinon的stub方法。stub会覆盖原组件的method，所以测试运行的时候，console.log('handleCheckPhoneNumber is running.');并不会运行。

同时注意在renderIntoDocument之前进行stub，且引用TextInput.prototype.__reactAutoBindMap而不是TextInput。

建议采用spy方式，stub会继续覆盖后续测试中的该method。

```javascript
// Component
let React = require('react');

let TextInput = React.createClass({
	
	handleCheckPhoneNumber: function(){
		console.log('handleCheckPhoneNumber is running.');
	},

	render: function() {
		return (
			<input
				type="text" 
				className="textInput"
				onBlur={this.handleCheckPhoneNumber} />
		);
	}
});

module.exports = TextInput;
```

```javascript
// Test
let TextInput = require('./Textinput');

it('call handleCheckPhoneNumber on Blur', () => {
	var spy = sinon.stub(TextInput.prototype.__reactAutoBindMap, "handleCheckPhoneNumber");
	let comp = TestUtils.renderIntoDocument(
			<TextInput />
		);

	let textInput = TestUtils.findRenderedDOMComponentWithClass(comp, 'textInput');
	React.addons.TestUtils.Simulate.blur(textInput);
		
	expect(spy.called).to.be.true;
});
```

### 参考

http://sinonjs.org/docs/#stubs

http://stackoverflow.com/questions/24280428/stubbing-a-react-component-method-with-sinon