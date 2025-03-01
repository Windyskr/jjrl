<template>
	<view class="content">
		
	<view class="buttons">
	<button type="default" @click="openHsrl">检测日历</button>
	<button type="default" @click="openWzrl">上星日历</button>
	<button type="default" @click="openHsrl">第三日历</button>
	<button type="default" @click="openWzrl">第四日历</button>
	</view>
	
	</view>
</template>

<script>
	
export default {
	components: {
		
	},
	data() {
		return {
			
		};
	},
	onLoad() {},
	watch: {
		
	},
	methods: {
		
	}
};
</script>

<style>
.content {
	display: flex;
	justify-content: center;
}
.buttons {
	margin: 50rpx;
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
}
.buttons button{
	margin: 50rpx;
	height: 200rpx;
	width: 200rpx;
	display: inline-flex;
	justify-content: center;
	font-size: 40rpx;
}
</style>
