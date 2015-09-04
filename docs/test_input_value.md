# 测试input的value改变

```javascript
	it('update phoneNumber on change', ()=>{
		let comp = TestUtils.renderIntoDocument(
				<TextInput />
			);
		
		expect(comp.state.phoneNumber).to.equal(''); // initial phoneNumber

		console.log(new Date());
		let textInput = TestUtils.findRenderedDOMComponentWithClass(comp, 'textInput');

		React.addons.TestUtils.Simulate.change(textInput, {target: {value: '1355'}});
		expect(comp.state.phoneNumber).to.equal('1355'); 
	});
```


```javascript
let React = require('react');

let TextInput = React.createClass({
	getInitialState: function(){
		return {
			phoneNumber: ''
		}
	},

	handleCheckPhoneNumber: function(){
		console.log('handleCheckPhoneNumber is running.');
		
	},

	handleChangePhoneNumber: function(e){
		console.log('handleChangePhoneNumber is running.', e.target);
		this.setState({phoneNumber: e.target.value});
	},
	render: function() {
		return (
			<input
				type="text" 
				className="textInput"
				placeholder="手机号" 
				value={this.state.phoneNumber}
				onChange={this.handleChangePhoneNumber}
				onBlur={this.handleCheckPhoneNumber} />
		);
	}
});

module.exports = TextInput;
```
### 参考

https://developer.mozilla.org/en-US/docs/Web/Events/change

http://stackoverflow.com/questions/24730019/simulating-text-entry-with-reactjs-testutils