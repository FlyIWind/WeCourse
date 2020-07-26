<template>
	<view v-if="isLogin">
		<components v-show="PageCur=='component'"></components>
		<plugin v-show="PageCur=='about'"></plugin>
		<view class="cu-bar tabbar bg-white shadow foot">
			<view class="action" @click="NavChange" data-cur="component">
				<view class='cuIcon-cu-image'>
					<image :src="'/static/tabbar/component' + [PageCur=='component'?'_cur':''] + '.png'"></image>
				</view>
				<view :class="PageCur=='component'?'text-green':'text-gray'">课表</view>
			</view>
			<view class="action" @click="NavChange" data-cur="about">
				<view class='cuIcon-cu-image'>
					<image :src="'/static/tabbar/about' + [PageCur == 'about'?'_cur':''] + '.png'"></image>
				</view>
				<view :class="PageCur=='about'?'text-green':'text-gray'">我的</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
		return {
				PageCur: 'component',
				isLogin:false
			}
		},
		methods: {
			NavChange: function(e) {
				this.PageCur = e.currentTarget.dataset.cur
			}
		},mounted:function(){
			if(localStorage.getItem('username')==null||localStorage.getItem('password')==null){
				uni.navigateTo({
					url:'../login/login'
				})
			}else{
				this.isLogin = true;
			}
		}
	}
</script>

<style>

</style>
