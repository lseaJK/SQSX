<template>
	<view>
		我的支部
		<view>
			<u-button size="mini" type="error" ripple="true">
				<view>
					<!-- <u-icon name="gift-fill" size="46" color="#111111"></u-icon> -->
					发布组织活动
				</view>
			</u-button>
			<u-button size="mini" type="error" ripple="true">考勤管理</u-button>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		mounted() {
			uni.setNavigationBarColor({frontColor:'#ffffff', backgroundColor: '#d81e06'})
			uni.setNavigationBarTitle({title:"我的支部"})
		},
		methods: {

		}
	}
</script>

<style>

</style>
