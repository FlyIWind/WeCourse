<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true"><block slot="backText">返回</block><block slot="content">学籍信息</block></cu-custom>
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
		var socketOpen = false;
		var socketMsgQueue = [];
		var that = this;
		var photo = uni.connectSocket({
			url: config.service
		});
		photo.onOpen(function(res) {
			console.log('连接成功')
			socketOpen = true;
			photo.send({
				data: '{"Type":"photo","UserName":"'+localStorage.getItem('username')+'","PassWord":"'+localStorage.getItem('password')+'","Week":null}'
			});
		});
		photo.onError(function(e){
			alert('服务器连接失败！')
		})
		photo.onMessage(function(res) {
			if(res.data.indexOf('data:image/jpg;base64')!=-1){
				that.$data.userPhoto = res.data;
				photo.send({
					data: '{"Type":"account","UserName":"'+localStorage.getItem('username')+'","PassWord":"'+localStorage.getItem('password')+'","Week":null}'
				})
			}else{
				that.$data.userInfo = JSON.parse(res.data);
			}
			
		});
	}
}	
</script>

<style>

</style>
