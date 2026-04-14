<template>
	<view class="content">
		<button @click="openCamera()">Open Camera</button>
		<!-- 弹窗 扫描二维码后显示二维码信息 -->
		<uni-popup ref="popup" type="center">
			<view style="width: 40vh; height: 80vh; background-color: white;">
				{{scanType}}
				<br>
				{{scanResult}}
			</view>
		</uni-popup>
	</view>
</template>

<script setup>
	import {
		ref,
		onMounted
	} from 'vue'

	const popup = ref(null)
	const scanType = ref('')
	const scanResult = ref('')

	const openCamera = () => {
		scanType.value = ''
		scanResult.value = ''
		uni.scanCode({
			scanType: ['qrCode'],
			success: function(res) {
				scanType.value = res.scanType
				scanResult.value = res.result
				popup.value.open()
			}
		});
	}

	onMounted(() => {
		console.log('init...')
	})
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 90vh;
	}
</style>