<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true"><block slot="backText">返回</block><block slot="content">考试成绩</block></cu-custom>
		<view class="cu-load load-modal" v-if="isLoading">
			<view class="gray-text">加载中...</view>
		</view>
		<view v-for="ts in grades" class="cu-list menu sm-border margin-top">
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
					<text class="text-grey">所在学期：{{ts.CourseTerm}}</text>
				</view>
			</view>
			<view class="cu-item">
				<view class="content">
					<text class="text-grey">最终成绩：{{ts.CourseGrade}}</text>
					<text class="text-grey" style="margin-left: 50rpx;">换算绩点：{{ts.GradePoint}}</text>
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
				grades:null,
				isLoading:true
			}
		},
		mounted:function(){
		var that = this;
		uni.sendSocketMessage({
			data: '{"Type":"grade","UserName":"'+uni.getStorageSync('username')+'","PassWord":"'+uni.getStorageSync('password')+'","Week":null}'
		});
		uni.onSocketMessage(function(res){
			res.data = JSON.parse(res.data);
			if(res.data.Type=="grade"){
				res.data = res.data.Data;
				that.$data.grades = res.data;
				that.$data.isLoading = false;
			}
		})
	}
}	
</script>

<style>

</style>
