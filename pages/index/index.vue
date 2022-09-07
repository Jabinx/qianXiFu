<template>
	<view class="content" catchtouchmove=“true”>
		<view class="xuan">
			<u-subsection :list="list" mode="button" :current="curNow" activeColor="#000000" @change="sectionChange">
			</u-subsection>
		</view>
		<!-- 旧换新 -->
		<view class="main" v-if="curNow">
			<text class="gouMaiText">新料重量（克）：</text>
			<view class="uinput">
				<u--input placeholder="请输入新料克数" border="bottom" clearable v-model="xinvalue" type="number"
					fontSize="20px">
				</u--input>
			</view>
			<text class="gouMaiText">旧料重量（克）：</text>
			<view class="uinput">
				<u--input placeholder="请输入旧料克数" border="bottom" clearable v-model="jiuvalue" type="number"
					fontSize="20px">
				</u--input>
			</view>
			<u-button type=" primary" text="确定" color="#000000" style="margin-top: 100rpx;" @click="huanok">
			</u-button>
		</view>
		<!-- 按克买 -->
		<view class="main" v-else>
			<text class="gouMaiText" style="flex: 9;">购买重量（克）：</text>
			<view class=" uinput">
				<u--input placeholder="请输入购买克数" border="bottom" clearable v-model="value" type="number" fontSize="20px">
				</u--input>
			</view>
			<view class="gongfei">
				<navigator url="/pages/shezhi/shezhi" class="gongfiezi"><text>每件的额外需加的工费（元）：</text></navigator>
				<view class="shurugongfei">
					<u--input placeholder="请输入工费" border="bottom" clearable v-model="value2" type="number"
						inputAlign="center " fontSize="20px">
					</u--input>
				</view>
			</view>
			<view class="xuanzhe" style="margin-top: 35rpx;display: flex;">
				黄金品类：
				<u-radio-group v-model="radiovalue" placement="row" @change="groupChange" style="margin-left: 10rpx;">
					<u-radio v-for="(item, index) in radiolist" :key="index" :label="item.name" :name="item.name"
						size="35rpx" style="margin-right: 40rpx;" labelSize="30rpx" activeColor="#000000"
						shape="square">
					</u-radio>
				</u-radio-group>
			</view>
			<u-button type=" primary" text="确定" color="#000000" style="margin-top: 100rpx;" @click="maiok">
			</u-button>
		</view>
		<u-modal :show="jieguoshow" :title='"总价格为:  ￥"+content' :closeOnClickOverlay="true" :zoom="false"
			confirmColor="#000000" @confirm="guanbi"></u-modal>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: ['按克买', '旧换新'],
				curNow: 0,
				show: false,
				value: '',
				value2: 0,
				radiolist: [{
						name: '万足金',
						disabled: false
					},
					{
						name: '千足金',
						disabled: false
					}
				],
				radiovalue: '万足金',
				xuandeshi: 1,
				xinvalue: '',
				jiuvalue: '',
				jieguoshow: false,
				content: 0
			}
		},
		onLoad() {

		},
		methods: {
			sectionChange(index) {
				this.curNow = index;
			},
			groupChange(n) {
				if (n === '千足金') {
					this.xuandeshi = 0
				} else {
					this.xuandeshi = 1
				}
			},
			maiok() {
				let x = 0
				if (this.xuandeshi) {
					uni.getStorage({
						key: 'cwang',
						success: (res) => {
							x = res.data
						}
					})
				} else {
					uni.getStorage({
						key: 'cqian',
						success: (res) => {
							x = res.data
						}
					})
				}
				this.content = x * this.value + this.value2 * 1
				this.jieguoshow = true
			},
			huanok() {
				let jiu = 0;
				let xin = 0;
				let bu = 0;
				uni.getStorage({
					key: 'cjiu',
					success: (res) => {
						jiu = res.data
					}
				})
				uni.getStorage({
					key: 'cxin',
					success: (res) => {
						xin = res.data
					}
				})
				uni.getStorage({
					key: 'cbu',
					success: (res) => {
						bu = res.data
					}
				})
				let xinvalue = parseFloat(this.xinvalue)
				let jiuvalue = parseFloat(this.jiuvalue)
				if (jiuvalue >= xinvalue) {
					this.content = parseInt(this.xinvalue * bu - (this.jiuvalue - this.xinvalue) * jiu)
				} else {
					this.content = parseInt((this.xinvalue - this.jiuvalue) * xin + this.jiuvalue * bu)
				}
				this.jieguoshow = true
			},
			guanbi() {
				this.jieguoshow = false
			}
		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.xuan {
		width: 700rpx;
		margin-left: auto;
		margin-right: auto;
		margin-top: 26rpx;
	}

	.main {
		width: 700rpx;
		margin-left: auto;
		margin-right: auto;
		margin-top: 50rpx;

		.uinput {
			margin-top: 25rpx;
			margin-bottom: 25rpx;
		}

		.gongfei {
			display: flex;

			.gongfiezi {
				margin-top: 20rpx;
			}

			.shurugongfei {
				width: 250rpx;
			}
		}
	}
</style>
