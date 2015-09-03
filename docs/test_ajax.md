# 测试Ajax

用sinon.sub可以模拟ajax请求，不需要服务器的测试，整个世界都清静了。

以下介绍了如何用sinon.sub模拟ajax请求的成功和失败的情况。

### Files

    app/src/PackageInfo.js
    app/test/PackageInfo-test.js

### PackageInfo-test.js
```javascript
var $ = require('jquery');
var React = require('react/addons');
var TestUtils = React.addons.TestUtils;

var PackageInfo = require('../src/PackageInfo');

describe('Load datas from ajax:', function(){
		var pInfo, app;
		beforeEach(function(){
			pInfo = { 
				package_number: 1, 
				package_point: 'Vocabulary', 
				package_hint: 'Write the parts of speech for each of the <u>underlined</u> words.'
			};

			app = TestUtils.renderIntoDocument(
				<PackageInfo />
			);
		});

		it('should load data from ajax when success.', function(){

			// Give a fake success return for $.ajax loading
			sinon.stub($, "ajax").yieldsTo("success", pInfo);
			
			// Use app.func to run func inside component
			app.loadPackageInfo('packageInfo.load', '/data/packageinfo/load', 2);

			// restore $.ajax from faking
			$.ajax.restore();
			
			expect(app.state.data).to.equal(pInfo);
		});

		it('should log warnings when failed.', function(){
			// Give a fake throws return for $.ajax loading
			sinon.stub($, "ajax").yieldsTo("error", "xhr", "simulate", "error");

			// Use app.func to run func inside component
			app.loadPackageInfo('packageInfo.load', '/data/packageinfo/load', 2);

			// restore $.ajax from faking
			$.ajax.restore();			
		});
	});
```
### PackageInfo.js
```javascript
var $ = require('jquery');
var React = require('react');

var PackageInfo = React.createClass({
	loadPackageInfo: function(msg, url, package_id){
		$.ajax({
			url: url + package_id,
			dataType: 'json',
			success: function(data){
				this.setState({data: data});
			}.bind(this),
			error: function(xhr, status, err){
				console.error(url, status, err.toString());
			}.bind(this)
		});
	},

	render: function(){
		return (
			<div className="packageInfo" >
				{this.state.data.package_number+ ". "}
				{this.state.data.package_point}
				<br />
				{this.state.data.package_hint}
			</div>
		);
	}
});

module.exports = PackageInfo;
```
### Notes
 1. 代码是从源程序中裁剪的，没有测试。
 1. 在多个ajax状态测试中，$.ajax.restore(); 不能包裹在after(function(){...})里，会报错。
 1. ajax error时候的测试，没有用expect检测，还不会。只能人肉去看log。