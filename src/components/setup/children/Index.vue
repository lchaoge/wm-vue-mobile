<template>
	<view-box ref="viewBox" class="setupIndex">
		<x-header :left-options="{showBack: false}" slot="header">
			<router-link slot="left" class="left-arrow" :to="{name:'userinfoLink'}"></router-link>
			设置
		</x-header>
		<div style="margin-top: 46px;">
		    <group class="mt10">
		      	<cell title="个人资料" is-link :link="{name:'setupUserInfoLink'}"></cell>
		      	<cell title="账号管理" is-link></cell>
		    </group>
		    <group class="mt10">
		      	<x-switch title="夜间模式"></x-switch>
		      	<x-switch title="中英切换" :value="true"></x-switch>
				<cell title="清除缓存"></cell>
			</group>
			<group class="mt10">
		      	<cell title="版本信息" value="9.6.8.2"></cell>
		      	<cell title="意见反馈" is-link></cell>
		    </group>
		    <group class="signout-box mt10" v-if="isLogin">
		    	<x-button type="warn" @click.native="exitLogon">退出</x-button>
		    </group>
		</div>
	</view-box>
</template>

<script>
	import {ViewBox,Group,XHeader,Cell,XSwitch,XButton} from 'vux'
	export default {
		components: {
			ViewBox,
			XButton,
			XSwitch,
			XHeader,
		  	Group,
		   	Cell
		},
		data () {
		    return {
		    	
		    }
		},
		beforeRouteEnter:(to,from ,next)=>{
			next((vm)=>{
				let isLogin = vm.$store.getters.isLogin
				if(!isLogin){
					vm.$router.push({name:'loginLink'})
				}
			})
		},
		computed:{
			currentUser(){
				return this.$store.getters.currentUser
			},
			isLogin(){
				return this.$store.getters.isLogin
			}
		},
		methods:{
			exitLogon(){
				this.$store.dispatch("setUser",null)
				this.$router.push({
					name:'loginLink'
				})
			}
		}
	}
</script>

<style>
	.signout-box{
		text-align: center;
		padding: 0 30%;
	}
</style>