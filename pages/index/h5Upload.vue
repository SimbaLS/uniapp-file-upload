<template>
	<view class="uni-form">
		<view>
			<form @submit="formSubmit" @reset="formReset">
				<view class="uni-form-item uni-column">
					<view class="title">名称</view>
					<input class="uni-input" name="name" placeholder="项目名称" />
				</view>
				<view class="uni-form-item uni-column">
					<view class="title">描述</view>
					<input class="uni-input" name="desc" placeholder="项目描述" />
				</view>
				<view class="uni-form-item uni-column">
					<button type="primary" plain="true" @tap="clickFileUpload">附件上传</button>
					<text>{{fileInfo}}</text>
				</view>
				<view class="uni-btn-v">
					<button type="primary" form-type="submit">Submit</button>
					<button type="default" form-type="reset">Reset</button>
				</view>
			</form>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				fileInfo: ''
			}
		},
		onLoad(option) {
			// 接收H5页面，跳转页面url传递数据
			if (option.fileData) {
				this.fileInfo = '页面跳转传递数据：' + option.fileData
				uni.showModal({
					content: this.fileInfo,
					showCancel: false
				});
			}
		},
		methods: {
			formSubmit: function(e) {
				// 一：从store中取出文件数据，并清理
				// 二：取调整页面url传递文件数据
				console.log('form发生了submit事件，携带数据为：' + JSON.stringify(e.detail.value))
				var formdata = e.detail.value
				uni.showModal({
					content: '表单数据内容：' + JSON.stringify(formdata),
					showCancel: false
				});
			},
			formReset: function(e) {
				console.log('清空数据')
			},
			clickFileUpload() {
				uni.navigateTo({
					url: './fileUpload',
				})
			}
		}
	}
</script>

<style>
	.uni-form {
		margin: 50rpx;
	}
	.uni-form-item .title {
		padding: 20rpx 0;
	}
	.uni-btn-v {
		padding-top: 30rpx;
	}
</style>
