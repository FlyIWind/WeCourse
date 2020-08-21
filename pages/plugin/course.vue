<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true"><block slot="backText">返回</block><block slot="content">在读课程</block></cu-custom>
		<view class="cu-load load-modal" v-if="isLoading">
			<view class="gray-text">加载中...</view>
		</view>
		<view v-for="ts in teachers" class="cu-list menu sm-border margin-top">
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">课程编号：{{ts.CourseID}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">课程名称：{{ts.CourseName}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">课程学分：{{ts.CourseCredit}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">任课教师：{{ts.CourseTeacher}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import config from '../../config.js'
	import socket from '../../js_sdk/plus-websocket/index.js'
	
	export default {
		data(){
			return{
				teachers:null,
				isLoading:true
			}
		},
		mounted:function(){
		var that = this;
		uni.sendSocketMessage({
			data: '{"Type":"teacher","UserName":"'+uni.getStorageSync('username')+'","PassWord":"'+uni.getStorageSync('password')+'","Week":null}'
		});
		uni.onSocketMessage(function(res){
			res.data = JSON.parse(res.data);
			if(res.data.Type=="teacher"){
				res.data = res.data.Data;
				that.$data.teachers = res.data;
				that.$data.isLoading = false;
			}
		})
	}
}	
</script>

<style>

</style>
