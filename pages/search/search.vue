<template>
	<view>
		搜索页
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		//监听原生标题栏搜索按钮点击事件
		onNavigationBarButtonTap(e){
			if(e.index == 0){
				uni.navigateBack({
					delta:1,
				})
			}
		},
		//监听输入变化
		onNavigationBarSearchInputChanged(e){
console.log(JSON.stringify(e.text))
		},
		//监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。	
		onNavigationBarSearchInputConfirmed(e){
			console.log(JSON.stringify(e.text))
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
