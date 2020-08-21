<template>
	<view>
		<view class="cu-modal" :class="modalName=='Modal'?'show':''">
			<view class="cu-dialog">
				<view class="cu-bar bg-white justify-end">
					<view class="content">登录失败</view>
					<view class="action" @tap="hideModal">
						<text class="cuIcon-close text-red"></text>
					</view>
				</view>
				<view class="padding-xl">
					{{alertmsg}}
				</view>
			</view>
		</view>
		<image src="/static/componentBg.png" mode="widthFix" class="response"></image>
		<h1 class="logintitle">登录</h1>
		<view class="input-group">
			<view class="input-row border">
				<text class="title">账号：</text>
				<input class="m-input" type="text" clearable focus  placeholder="请输入账号" v-model="username"></input>
			</view>
			<view class="input-row">
				<text class="title">密码：</text>
				<input class="m-input" type="password" displayable  placeholder="请输入密码" v-model="password"></input>
			</view>
		</view>
		<view class="text-center" style="margin-top: 20rpx;">
			<view class="cu-tag line-blue">注：账号密码与教务系统相同</view>
		</view>
		<view class="text-center" style="margin-top: 20rpx;">
			<button class="cu-btn lines-blue  shadow" :loading="isLogin" @click="login()">登录</button>
		</view>
		
	</view>
</template>

<script>
	import config from '../../config.js'
	
	export default{
		data(){
			return{
				username:null,
				password:null,
				isLogin:false,
				modalName: null,
				alertmsg:null,
			}
		},
		mounted:function(){
			var that = this
			uni.onSocketMessage(function(res) {
				console.log(res.data);
				res.data = JSON.parse(res.data);
				if(res.data.Type=="login"){
						res.data = res.data.Data
						if(res.data=="登录成功"){
							uni.setStorage({key:'username',data:that.username});
							uni.setStorage({key:'password',data:that.password});
							uni.redirectTo({
								url:'../index/index'
							})
						}else{
							//alert('登录失败！');
							that.alertmsg = "登录失败，请检查用户名或密码是否正确";
							that.modalName = "Modal";
							that.isLogin = false;
						}
				}
			}
			);
		}
		,methods:{
			login:function(){
				if(!this.isLogin){
					if(this.username==null||this.password==null||this.username==""||this.password==""||this.username.length==0||this.password.length==0){
						//alert('用户名或密码不能为空！');
						this.alertmsg = "用户名或密码不能为空";
						this.modalName = "Modal";
						return;
					}
					this.isLogin = true;
					var that = this;
					function sendSocketMessage(msg) {
						uni.sendSocketMessage({
							data: msg
						});
					}
					sendSocketMessage('{"Type":"login","UserName":"'+that.username+'","PassWord":"'+that.password+'","Week":1}')
				}
			},showModal(e) {
				this.modalName = "Modal";
			},
			hideModal(e) {
				this.modalName = null
			},
		}
	}
</script>

<style>
	.logintitle{
		background: linear-gradient(to left, lightblue, blue);
		        -webkit-background-clip: text;
		        color: transparent;
		text-align: center;
	}
</style>
