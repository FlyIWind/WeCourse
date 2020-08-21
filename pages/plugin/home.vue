<template name="components">
	<view>
		<cu-custom bgImage="https://image.weilanwl.com/color2.0/plugin/cjkz2329.jpg">
			<block slot="content">
				<h3>我的微课表</h3>
			</block>
		</cu-custom>
		<view class="cu-list menu sm-border card-menu margin-top" @click="gotoStuinfo()">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-profile text-grey"></text>
					<text class="text-grey">学籍信息</text>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu margin-top" @click="gotoCourse()">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-write text-grey"></text>
					<text class="text-grey">在读课程</text>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu margin-top" @click="gotoGrade()">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-punch text-grey"></text>
					<text class="text-grey">考试成绩</text>
				</view>
			</view>
		</view>
	
		<view class="cu-list menu sm-border card-menu margin-top" @click="gotoLogin()">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-usefull text-grey"></text>
					<text class="text-grey">切换账号</text>
				</view>
			</view>
		</view>
		<view style="text-align: center;padding-top: 30px;">
			<image style="width: 250rpx;height: 250rpx;" src="https://www.syfit.cn/img/barcode.png"></image><br/>
			<text style="color: #39B54A;">分享此小程序给你的朋友</text>
		</view>
		
	</view>
</template>

<script>
	export default {
		methods:{
			gotoStuinfo:function(){
				uni.navigateTo({
					url:'../plugin/stuinfo'
				})
			},gotoCourse:function(){
				uni.navigateTo({
					url:'../plugin/course'
				})
			},gotoGrade:function(){
				uni.navigateTo({
					url:'../plugin/grade'
				})
			},gotoLogin:function(){
				uni.navigateTo({
					url:'../login/login'
				})
			}
		}
	}
</script>

<style>

</style>
