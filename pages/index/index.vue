<template>
	<view class="content">
		<view class="description">
			<uni-title type="h2" title="使用说明 "></uni-title>
			<view>1.请先选择你的隔离开始和结束日期</view>
			<view>2.在日历上点击你做核酸的日期</view>
			<view>3.点击导出日历，导出属于你的核酸日历！</view>
		</view>

		<view class="pickerContainer">
			<view class="time">隔离开始时间</view>
			<view class="time">隔离结束时间</view>

			<view class="picker-view"><uni-datetime-picker type="date" :clear-icon="false" v-model="start" @maskClick="maskClick" /></view>
			<view class="picker-view"><uni-datetime-picker type="date" :clear-icon="false" v-model="end" @maskClick="maskClick" /></view>
		</view>

		<Calender :list="list" :date="date" :time_key="time_key" @day_change="day_change_fun" :start="start" :end="end" @date_change="date_change_fun" :key="key" />

		<view class="buttons">
			<button type="default" @click="downPhoto">导出日历</button>
			<button type="default" @click="share">分享</button>
		</view>

		<view class="icp">来自 https://hsrl.mhatp.cn/</view>
		<view class="icp">赣ICP备20002039号-1</view>2

		<!-- <a target="_blank" href="https://beian.miit.gov.cn/">
		          赣ICP备20002039号-1
		  </a> -->
	</view>
</template>

<script>
import Calender from '@/components/Calender/Calender.vue';
export default {
	components: {
		Calender
	},
	data() {
		return {
			// 当前的日期
			date: '',
			// 存放时间的key值
			time_key: '',
			// 已经签到的数据列表
			list: [],
			// 存放隔离的起止日期
			start: '2022-03-18',
			end: '2022-05-10',
			key: 0
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
		};
	},
	onLoad() {},
	// 方法
	watch: {
		start(newval) {
			// console.log('单选:', this.start);
			this.key += 1;
		},
		end(newval) {
			// console.log('单选:', this.end);
			this.key += 1;
		}
	},
	methods: {
		// 点击天
		day_change_fun(day) {
			// console.log(JSON.parse(JSON.stringify(day)));
			// console.log(JSON.parse(JSON.stringify(day)).nyr)
			uni.showToast({
				icon: 'none',
				position: 'top',
				title: JSON.parse(JSON.stringify(day)).nyr,
				duration: 300
			});

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
			} else {
				if (time_key) {
					let obj = {};
					obj[time_key] = day.nyr;
					this.list.splice(this.list.indexOf(obj), 1);
				} else {
					this.list.splice(this.list.indexOf(day.nyr), 1);
				}
			}
		},
		// 日期改变时触发
		date_change_fun(date) {
			// 更新日期
			this.date = date;
			// 根据日期获取已经签到的列表然后赋值
			// 存放时间的key值
			let time_key = this.time_key;
			// if (time_key) {
			// 	this.list.push({
			// 		time: '01'
			// 	});
			// } else {
			// 	this.list.push('01');
			// }
		},
		maskClick(e) {
			// console.log('----maskClick事件:', e);
		},
		downPhoto() {
			uni.showToast({
				icon: 'none',
				title: '功能施工中',
				duration: 500
			});

			console.log('导出图片');
		},
		share() {
			uni.showToast({
				icon: 'none',
				title: '功能施工中',
				duration: 500
			});
			console.log('分享');
		}
	}
};
</script>

<style>
.description {
	display: flex;
	flex-direction: column;
	align-items: center;
	margin: 20rpx;
}

.pickerContainer {
	display: flex;
	flex-wrap: wrap;
	justify-content: left;
	margin-bottom: 10rpx;
}

.pickerContainer .time {
	width: 50%;
}
.pickerContainer .picker-view {
	width: 50%;
}

.buttons {
	display: flex;
	justify-content: center;
}

.buttons button {
	width: 300rpx;
	margin: 20rpx;
}

.icp {
	display: flex;
	justify-content: center;
	margin: 10rpx;
}
</style>
