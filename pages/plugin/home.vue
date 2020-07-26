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
		<view class="cu-list menu sm-border card-menu margin-top">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-write text-grey"></text>
					<text class="text-grey">在读课程</text>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu margin-top">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-punch text-grey"></text>
					<text class="text-grey">考试成绩</text>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu margin-top">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-remind text-grey"></text>
					<text class="text-grey">考试安排</text>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu margin-top">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-refresh text-grey"></text>
					<text class="text-grey">检查更新</text>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu margin-top">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-repair text-grey"></text>
					<text class="text-grey">意见反馈</text>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu margin-top">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-hot text-grey"></text>
					<text class="text-grey">关于程序</text>
				</view>
			</view>
		</view>
		<view class="cu-list menu sm-border card-menu margin-top">
			<view class="cu-item arrow">
				<view class="content">
					<text class="cuIcon-usefull text-grey"></text>
					<text class="text-grey">切换账号</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		methods:{
			gotoStuinfo:function(){
				console.log('cao')
				uni.navigateTo({
					url:'../plugin/stuinfo'
				})
			}
		}
	}
</script>

<style>

</style>
