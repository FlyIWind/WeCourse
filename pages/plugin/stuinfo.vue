<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true"><block slot="backText">返回</block><block slot="content">学籍信息</block></cu-custom>
		<view class="cu-load load-modal" v-if="isLoading">
			<view class="gray-text">加载中...</view>
		</view>
		<view class="cu-list menu sm-border margin-top">
			<view style="text-align: center;">
				<image class="cu-avatar radius xl" :src="userPhoto"></image>
			</view>
			
		</view>
		
		<view class="cu-list menu sm-border margin-top">
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">姓名：{{userInfo.FullName}}</text>
				</view>
				<view class="content">
					<text class="text-grey">性别：{{userInfo.Sex}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">入学时间：{{userInfo.StartTime}}</text>
				</view>
				<view class="content">
					<text class="text-grey">毕业时间：{{userInfo.EndTime}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">学历类型：{{userInfo.Type}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">二级学院：{{userInfo.System}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">专业名称：{{userInfo.Specialty}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">行政班级：{{userInfo.Class}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import config from '../../config.js'
	
	export default {
		data(){
			return{
			isLoading:true,
			userPhoto:'../../static/logo.png',
			userInfo:
				{
					"FullName": "获取中...",
					"EnglishName": "获取中...",
					"Sex": "获取中...",
					"StartTime": "获取中...",
					"EndTime": "获取中...",
					"SchoolYear": "获取中...",
					"Type": "获取中...",
					"System": "获取中...",
					"Specialty": "获取中...",
					"Class": "获取中..."
				}
			}
		},
		mounted:function(){
		var that = this;
		uni.sendSocketMessage({
			data: '{"Type":"photo","UserName":"'+uni.getStorageSync('username')+'","PassWord":"'+uni.getStorageSync('password')+'","Week":null}'
		});
		uni.onSocketMessage(function(res) {
			res.data = JSON.parse(res.data);
			if(res.data.Type=="photo"){
				res.data = res.data.Data;
				that.$data.userPhoto = res.data;
				uni.sendSocketMessage({data: '{"Type":"account","UserName":"'+uni.getStorageSync('username')+'","PassWord":"'+uni.getStorageSync('password')+'","Week":null}'
				});
			}
			if(res.data.Type=="account"){
				res.data = res.data.Data;
				that.$data.userInfo = res.data;
				that.$data.isLoading = false;
			}
			
		});
	}
}	
</script>

<style>

</style>
