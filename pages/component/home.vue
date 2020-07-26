<template name="components">
	<view>
<!-- 		<view v-if="isLoading" class="bg-white page">
			<image src="/static/componentBg.png" mode="widthFix" class="response"></image>
			<h1 style="text-align: center;" class="notice">正在加载课程表...</h1>
			<image src="https://image.weilanwl.com/gif/loading-white.gif" mode="aspectFit" class="gif-white response"></image>
		</view> -->
		<view class="cu-load load-modal" v-if="isLoading">
			<view class="gray-text">加载中...</view>
		</view>
		<view style="background: url(../../static/background.jpeg) no-repeat;background-size: 100%;background-position: 0px 120px;">
			<scroll-view scroll-y class="page">
				<div style="position: fixed;z-index: 999;top:25%; left:23.5%;width: 460px;">
					<view class="cu-tag line-white text-lg" @click="updownWeek(1)">-</view><view class="cu-tag line-white text-lg" @click="changeWeek()">当前教学周：第{{week}}周</view><view class="cu-tag line-white text-lg" @click="updownWeek(0)">+</view></div>
				<image src="/static/componentBg.png" mode="widthFix" class="response"></image>
				<view id="coursesTable">
					<div id="coursesTable" style="background: rgba(255,255,255, 0.3);;overflow: hidden;">
						<div id="courseWrapper" style="position: relative; padding-left: 40px;">
							<div style="overflow: hidden;" class="Courses-head">
								<div class="Courses-head-1" style="float: left; box-sizing: border-box; white-space: nowrap; width: 20%;text-align: center;">周一</div>
								<div class="Courses-head-2" style="float: left; box-sizing: border-box; white-space: nowrap; width: 20%;text-align: center;">周二</div>
								<div class="Courses-head-3" style="float: left; box-sizing: border-box; white-space: nowrap; width: 20%;text-align: center;">周三</div>
								<div class="Courses-head-4" style="float: left; box-sizing: border-box; white-space: nowrap; width: 20%;text-align: center;">周四</div>
								<div class="Courses-head-5" style="float: left; box-sizing: border-box; white-space: nowrap; width: 20%;text-align: center;">周五</div>
							</div>
							<div class="Courses-content"  style="border: rgba(0,0,0, 0.4) 1rpx solid;">
								<div v-for="n in 5">
									<ul style="list-style: outside none none; padding: 0px; margin: 0px; min-height: 50px;">
										<li v-show="!isLoading" v-for="item in Course" style="float: left; width: 20%; height: 50px; box-sizing: border-box; position: relative;" :style="[{animation: 'show ' + ((0+1)*0.2+1) + 's 1'}]">
											<span v-if="item[n-1]!=null" :style="{background:item[n-1].Color}" @click="showMessage(item[n-1],n-1)" style="position: absolute; z-index: 9; width: 100%; height: 100px; left: 0px; top: 0px;color: rgb(255, 255, 255);overflow: hidden;"
											 class="course-hasContent">{{item[n-1].CourseName}}<br />{{item[n-1].TeacherName}}<br />{{item[n-1].RoomName}}</span>
										</li>
									</ul>
									<ul style="list-style: outside none none; padding: 0px; margin: 0px; min-height: 50px;"></ul>
								</div>
							</div>
							<div class="Courses-leftHand" style="position: absolute; left: 0px; top: 0px; width: 40px;text-align: center;">
								<div class="left-hand-TextDom" style="height: 29px; box-sizing: border-box;"></div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-1">
									<p style="margin: 0px;" class="left-hand-index">1</p>
									<p style="margin: 0px;" class="left-hand-name">8:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-2">
									<p style="margin: 0px;" class="left-hand-index">2</p>
									<p style="margin: 0px;" class="left-hand-name">9:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-3">
									<p style="margin: 0px;" class="left-hand-index">3</p>
									<p style="margin: 0px;" class="left-hand-name">10:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-4">
									<p style="margin: 0px;" class="left-hand-index">4</p>
									<p style="margin: 0px;" class="left-hand-name">11:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-5">
									<p style="margin: 0px;" class="left-hand-index">5</p>
									<p style="margin: 0px;" class="left-hand-name">12:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-6">
									<p style="margin: 0px;" class="left-hand-index">6</p>
									<p style="margin: 0px;" class="left-hand-name">14:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-7">
									<p style="margin: 0px;" class="left-hand-index">7</p>
									<p style="margin: 0px;" class="left-hand-name">15:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-8">
									<p style="margin: 0px;" class="left-hand-index">8</p>
									<p style="margin: 0px;" class="left-hand-name">16:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-9">
									<p style="margin: 0px;" class="left-hand-index">9</p>
									<p style="margin: 0px;" class="left-hand-name">17:30</p>
								</div>
								<div style="width: 100%; height: 50px; box-sizing: border-box;" class="left-hand-10">
									<p style="margin: 0px;" class="left-hand-index">10</p>
									<p style="margin: 0px;" class="left-hand-name">18:30</p>
								</div>
							</div>
						</div>
					</div>
				</view>
				<view class="cu-tabbar-height"></view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	import config from '../../config.js'
	
	export default {
		data() {
			return {
				isLoading: true,
				Course: [
					[null, null, null, null, null],
					[null, null, null, null, null],
					[null, null, null, null, null],
					[null, null, null, null, null],
					[null, null, null, null, null]
				],
				week:1
			};
		},
		methods: {
			showMessage: function(item, time) {
				var TimeOfTheDay = '';
				if (time == 0) {
					TimeOfTheDay = '1,2';
				}
				if (time == 1) {
					TimeOfTheDay = '3,4';
				}
				if (time == 2) {
					TimeOfTheDay = '5,6';
				}
				if (time == 3) {
					TimeOfTheDay = '7,8';
				}
				if (time == 4) {
					TimeOfTheDay = '9,10';
				}
				alert("课程名称：" + item.CourseName + "\r\n" + "教师姓名：" + item.TeacherName + "\r\n" + "上课时间：" + TimeOfTheDay + "节\r\n" +
					"上课地点：" + item.RoomName)
			},updownWeek:function(UpDown){
				if(UpDown==0){
					this.week++;
				}else{
					this.week--;
					if(this.week<=0){
						this.week = 1;
					}
				}
				uni.sendSocketMessage({
					data: '{"Type":"course","UserName":"'+localStorage.getItem('username')+'","PassWord":"'+localStorage.getItem('password')+'","Week":'+this.week+'}'
				});
				this.isLoading = true;
			},changeWeek:function(){
				let inputweek = prompt("请输入教学周",this.week);
				inputweek = parseInt(inputweek);
				if(inputweek>=1){
					this.week = inputweek;
					uni.sendSocketMessage({
						data: '{"Type":"course","UserName":"'+localStorage.getItem('username')+'","PassWord":"'+localStorage.getItem('password')+'","Week":'+this.week+'}'
					});
					this.isLoading = true;
				}
			}			
		},
		mounted: function() {
			var socketOpen = false;
			var socketMsgQueue = [];
			var colorList = ['#f05261', '#48a8e4', '#ffd061', '#52db9a', '#70d3e6', '#52db9a', '#3f51b5', '#f3d147', '#4adbc3',
				'#673ab7', '#f3db49', '#76bfcd', '#b495e1', '#ff9800', '#8bc34a', '#f05261', '#48a8e4', '#ffd061', '#52db9a',
				'#70d3e6', '#52db9a', '#3f51b5', '#f3d147', '#4adbc3', '#673ab7', '#f3db49', '#76bfcd', '#b495e1', '#ff9800',
				'#8bc34a', '#f05261', '#48a8e4', '#ffd061', '#52db9a', '#70d3e6', '#52db9a', '#3f51b5', '#f3d147', '#4adbc3',
				'#673ab7', '#f3db49', '#76bfcd', '#b495e1', '#ff9800', '#8bc34a', '#f05261', '#48a8e4', '#ffd061', '#52db9a',
				'#70d3e6', '#52db9a', '#3f51b5', '#f3d147', '#4adbc3', '#673ab7', '#f3db49', '#76bfcd', '#b495e1', '#ff9800',
				'#8bc34a'
			];
			var courseColor = [];
			var that = this;
			uni.connectSocket({
				url: config.service
			});

			uni.onSocketOpen(function(res) {
				console.log('连接成功')
				socketOpen = true;
				for (var i = 0; i < socketMsgQueue.length; i++) {
					sendSocketMessage(socketMsgQueue[i]);
				}
				socketMsgQueue = [];
			});
			uni.onSocketError(function(e){
				alert('服务器连接失败！')
			})
			uni.onSocketMessage(function(res) {
				//console.log('收到服务器内容：' + res.data);
				
				if (res.data.length > 2) {
					try{
						res.data = JSON.parse(res.data)
					}catch(e){
						return;
					}
					that.Course = [
					[null, null, null, null, null],
					[null, null, null, null, null],
					[null, null, null, null, null],
					[null, null, null, null, null],
					[null, null, null, null, null]
				];
					
					if(res.data==null){
						//alert('课表数据为空！');
						that.$data.isLoading = false;
						return;
					}
					for (var i = 0; i < res.data.length; i++) {
						courseColor[i] = res.data[i].CourseName;
					}
					courseColor = Array.from(new Set(courseColor))
					var newcourseColor = [];
					for (var i = 0; i < courseColor.length; i++) {
						newcourseColor[courseColor[i]] = colorList[i];
					}
					for (var i = 0; i < res.data.length; i++) {
						var thisCourse = res.data[i];
						if (thisCourse.TimeOfTheDay == "1,2") {
							that.Course[thisCourse.DayOfTheWeek][0] = {
								"CourseName": thisCourse.CourseName,
								"TeacherName": thisCourse.TeacherName,
								"RoomName": thisCourse.RoomName,
								"Color": newcourseColor[thisCourse.CourseName]
							}
						}
						if (thisCourse.TimeOfTheDay == "3,4") {
							that.Course[thisCourse.DayOfTheWeek][1] = {
								"CourseName": thisCourse.CourseName,
								"TeacherName": thisCourse.TeacherName,
								"RoomName": thisCourse.RoomName,
								"Color": newcourseColor[thisCourse.CourseName]
							}
						}
						if (thisCourse.TimeOfTheDay == "5,6") {
							that.Course[thisCourse.DayOfTheWeek][2] = {
								"CourseName": thisCourse.CourseName,
								"TeacherName": thisCourse.TeacherName,
								"RoomName": thisCourse.RoomName,
								"Color": newcourseColor[thisCourse.CourseName]
							}
						}
						if (thisCourse.TimeOfTheDay == "7,8") {
							that.Course[thisCourse.DayOfTheWeek][3] = {
								"CourseName": thisCourse.CourseName,
								"TeacherName": thisCourse.TeacherName,
								"RoomName": thisCourse.RoomName,
								"Color": newcourseColor[thisCourse.CourseName]
							}
						}
						if (thisCourse.TimeOfTheDay == "9,10") {
							that.Course[thisCourse.DayOfTheWeek][4] = {
								"CourseName": thisCourse.CourseName,
								"TeacherName": thisCourse.TeacherName,
								"RoomName": thisCourse.RoomName,
								"Color": newcourseColor[thisCourse.CourseName]
							}
						}
					}
					console.log(that.Course);
					that.$forceUpdate();
					that.$data.isLoading = false;
				}else{
					if(res.data<=0){
						res.data = 1;
					}
					that.$data.week = res.data;
					uni.sendSocketMessage({
						data: '{"Type":"course","UserName":"'+localStorage.getItem('username')+'","PassWord":"'+localStorage.getItem('password')+'","Week":'+res.data+'}'
					});
				}
			});

			function sendSocketMessage(msg) {
				if (socketOpen) {
					uni.sendSocketMessage({
						data: msg
					});
				} else {
					socketMsgQueue.push(msg);
				}
			}
			sendSocketMessage('{"Type":"week","UserName":null,"PassWord":null,"Week":null}');//获取教学周
		}
	}
</script>

<style>
	.page {
		height: 100vh;
	}
	.notice{
		background: linear-gradient(to right, red, blue);
		        -webkit-background-clip: text;
		        color: transparent;
	}
</style>
