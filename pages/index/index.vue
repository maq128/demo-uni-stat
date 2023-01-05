<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">
				device_id: {{device_id}}
			</text>
			<text class="title">
				push_clientid: {{push_clientid}}
			</text>
			<text class="title">
				本程序开启了【uni统计】和【uniPush2.0】。
			</text>
			<text class="title">
				<a href="https://uniapp.dcloud.net.cn/uniCloud/uni-cloud-push/mate.html" target="_blank">官方文档</a>
				说 uni 统计模块在启动时会报送本设备的 device_id 和 push_client_id。
			</text>
			<text class="title">
				请检查云数据库 opendb-device 表里面的记录，可能 push_clientid 字段为空串，
				这将导致后续向本设备的 device_id 推送消息会失败。
			</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				device_id: '-',
				push_clientid: '-'
			}
		},
		onLoad() {
			var si = uni.getSystemInfoSync()
			this.device_id = si.deviceId
			uni.getPushClientId({
				success: (res) => {
					console.log('uni.getPushClientId success:', res)
					this.push_clientid = res.cid
				},
				fail: (err) => {
					console.log('uni.getPushClientId fail:', err)
					this.push_clientid = 'xxx'
				}
			})
		},
		methods: {
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		flex-direction: column;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: black;
		margin: 0.3em;
		line-break: anywhere;
	}
</style>
