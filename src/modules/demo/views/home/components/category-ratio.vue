<template>
	<div class="category-ratio">
		<div class="category-ratio__header">
			<span>党建活动类别占比</span>
		</div>

		<div class="category-ratio__container">
			<v-chart :option="chartOption" autoresize />
		</div>
	</div>
</template>

<script lang="ts" setup>
import { reactive } from "vue";

const chartOption = reactive({
	tooltip: {
		trigger: "item",
		formatter: "{a} <br/>{b}: {c} ({d}%)"
	},
	legend: {
		bottom: 30,
		left: "center",
		data: ["党课学习", "志愿服务", "主题党日", "红色教育", "党建会议"]
	},
	series: [
		{
			type: "pie",
			radius: ["50%", "60%"],
			center: ["50%", "40%"],
			avoidLabelOverlap: false,
			label: {
				show: false,
				position: "center"
			},
			emphasis: {
				label: {
					show: true,
					fontSize: "30",
					fontWeight: "bold"
				}
			},
			labelLine: {
				show: false
			},
			data: [
				{ value: 335, name: "党课学习" },
				{ value: 310, name: "志愿服务" },
				{ value: 234, name: "主题党日" },
				{ value: 135, name: "红色教育" },
				{ value: 500, name: "党建会议" }
			],
			itemStyle: {
				borderColor: "#fff",
				borderWidth: 4
			},
			roundCap: 1
		}
	]
});
</script>

<style lang="scss" scoped>
.category-ratio {
	&__header {
		display: flex;
		align-items: center;
		height: 50px;
		font-size: 15px;
		font-weight: bold;
		padding: 0 20px;
	}

	&__container {
		height: 385px;
		padding: 0 20px;
		box-sizing: border-box;

		.echarts {
			width: 100%;
		}
	}
}
</style>

