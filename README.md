## 使用说明：
| 属性名		| 类型			|  说明																	|
| --------		| -----:		| :----:																|
| date			| String		|  当前日期，格式支持YYYY-MM											|
| list			| Array			|  已经签到的时间列表，格式支持YYYY-MM-DD、MM-DD、DD					|
| time_key		|String			|如果已签到的时间列表是对象的数组，time_key表示对象中用来存放时间的key值|
| day_change	|    function	|  点击日期时调用（上月和下月不会触发）									|
| date_change	|    function	|  当前日期改变时调用													|

```html
	<qian-dao
		:list="list"
		:date="date"
		:time_key="time_key"
		@day_change="day_change_fun"
		@date_change="date_change_fun"
	></qian-dao>
```

```javascript
    export default {
		data() {
			return {
				// 当前的日期
				date: "",
				
				// 存放时间的key值
				time_key: "",
				// 已经签到的数据列表
				list: ["2020-05-10", "03-15", "20", "31"],
				
				// // 存放时间的key值
				// time_key: "time",
				// // 已经签到的数据列表
				// list: [{
				// 	time: "2020-05-10",
				// }, {
				// 	time: "03-15",
				// }, {
				// 	time: "20",
				// }, {
				// 	time: "31"
				// }],
			}
		},
		// 方法
		methods: {
			// 点击天
			day_change_fun(day) {
				console.log(JSON.parse(JSON.stringify(day)));
			
				// 存放时间的key值
				let time_key = this.time_key;
			
				// 如果没有签到（可以补签，需要补签的可以这么写）
				if (!day.click) {
					if (time_key) {
						let obj = {};
						obj[time_key] = day.nyr;
						this.list.push(obj);
					} else {
						this.list.push(day.nyr);
					}
				}
			
				// 如果今天没有签到(只签到今天的，如果只需要签到今天的可以这么写)
				// if (!day.click && day.type == "today") {
				// 	if (time_key) {
				// 		let obj = {};
				// 		obj[time_key] = day.nyr;
				// 		this.list.push(obj);
				// 	} else {
				// 		this.list.push(day.nyr);
				// 	}
				// }
			},
			// 日期改变时触发
			date_change_fun(date) {
				// 更新日期
				this.date = date;
			
				// 清空已经签到的列表
				this.list = [];
			
				// 根据日期获取已经签到的列表然后赋值
				// 存放时间的key值
				let time_key = this.time_key;
				if (time_key) {
					this.list.push({
						time: "01"
					});
				} else {
					this.list.push("01");
				}
			},
		},
	}
```

Tips:
  * 有啥问题和建议或者错误不足之处，还望各位大神指出。
  * 如果问题急的话+QQ：806834390。答案：真。

### 历史版本
----
### V1.0.0   2020-05-29
抽空重新整理了下，将事件处理放在了父组件中实现，注释写的还算明白，相信聪明的你能够看懂
### V1.1.0   2020-06-01
优化了下css
### V1.1.1   2020-10-26
对数据和布局进行了优化，新增年月选择，点击中间的年月触发
### V1.2.1   2020-10-30
由于项目需要，新增属性time_key，用来兼容签到列表是对象数组的情况，如果不是，不设置time_key即可
### V1.2.2   2020-11-03
根据使用反馈，将demo页面 /pages/index/index 修改为 /pages/qd_demo ,应该不会再覆盖了吧？
### V1.2.3   2021-09-04
根据使用反馈，新增时间戳判断，今天之后的日期点击将不再触发事件