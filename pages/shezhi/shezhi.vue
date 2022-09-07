<template>
	<view class="zhuti">
		<view class="biaoti">
			按克买设置：
		</view>
		<u-line></u-line>
		<view class="shezishuru">
			<text class="zi">万足金每克（元）：</text>
			<view style="width: 355rpx;">
				<u--input placeholder="请输入内容" border="bottom" clearable v-model="wang" inputAlign="center "
					@blur="wblur" type="number"></u--input>
			</view>
		</view>
		<view class="shezishuru">
			<text class="zi">千足金每克（元）：</text>
			<view style="width: 355rpx;">
				<u--input placeholder="请输入内容" border="bottom" clearable v-model="qian" type="number"
					inputAlign="center " @blur="qblur"></u--input>
			</view>
		</view>
		<view class="biaoti">
			旧换新设置：
		</view>
		<u-line></u-line>
		<view class="shezishuru">
			<text class="zi">旧料每克（元）：</text>
			<view style="width: 390rpx;">
				<u--input placeholder="请输入内容" border="bottom" clearable v-model="jiu" type="number" inputAlign="center "
					@blur="jblur"></u--input>
			</view>
		</view>
		<view class="shezishuru">
			<text class="zi">新料每克（元）：</text>
			<view style="width: 390rpx;">
				<u--input placeholder="请输入内容" border="bottom" clearable v-model="xin" type="number" inputAlign="center "
					@blur="xblur"></u--input>
			</view>
		</view>
		<view class="shezishuru">
			<text class="zi">旧换新每克补（元）：</text>
			<view style="width: 330rpx;">
				<u--input placeholder="请输入内容" border="bottom" clearable v-model="bu" type="number" inputAlign="center "
					@blur="bblur">
				</u--input>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				wang: '',
				qian: '',
				jiu: '',
				xin: '',
				bu: '',
			}
		},
		onShow() {
			uni.getStorage({
				key: 'cwang',
				success: (res) => {
					this.wang = res.data
				}
			})
			uni.getStorage({
				key: 'cqian',
				success: (res) => {
					this.qian = res.data
				}
			})
			uni.getStorage({
				key: 'cjiu',
				success: (res) => {
					this.jiu = res.data
				}
			})
			uni.getStorage({
				key: 'cxin',
				success: (res) => {
					this.xin = res.data
				}
			})
			uni.getStorage({
				key: 'cbu',
				success: (res) => {
					this.bu = res.data
				}
			})
		},

		methods: {
			wblur() {
				uni.setStorage({
					key: 'cwang',
					data: this.wang
				})
			},
			qblur() {
				uni.setStorage({
					key: 'cqian',
					data: this.qian
				})
			},
			jblur() {
				uni.setStorage({
					key: 'cjiu',
					data: this.jiu
				})
			},
			xblur() {
				uni.setStorage({
					key: 'cxin',
					data: this.xin
				})
			},
			bblur() {
				uni.setStorage({
					key: 'cbu',
					data: this.bu
				})
			},
		}
	}
</script>

<style lang="scss">
	.zhuti {
		width: 700rpx;
		margin-left: auto;
		margin-right: auto;
		// margin-top: 50rpx;
		// position: fixed;
		overflow: hidden;
	}

	.biaoti {
		// width: 100%;
		height: 60rpx;
		margin-top: 100rpx;
		border-left: 30rpx solid #000000;
		line-height: 50rpx;
		font-size: 50rpx;
		padding-left: 20rpx;
	}

	.shezishuru {
		display: flex;
		margin-left: 50rpx;
		margin-top: 25rpx;
		margin-bottom: 25rpx;

		.zi {
			margin-top: 20rpx;
		}
	}
</style>
