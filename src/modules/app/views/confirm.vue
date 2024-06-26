<template>
	<cl-crud ref="Crud">
		<cl-row>
			<!-- 刷新按钮 -->
			<cl-refresh-btn />
			<!-- 新增按钮 -->
			<cl-add-btn />
			<!-- 删除按钮 -->
			<cl-multi-delete-btn />
			<cl-flex1 />
			<!-- 关键字搜索 -->
			<cl-search-key />
		</cl-row>

		<cl-row>
			<!-- 数据表格 -->
			<cl-table ref="Table" />
		</cl-row>

		<cl-row>
			<cl-flex1 />
			<!-- 分页控件 -->
			<cl-pagination />
		</cl-row>

		<!-- 新增、编辑 -->
		<cl-upsert ref="Upsert" />
	</cl-crud>
</template>

<script lang="ts" name="app-confirm" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "订单名称",
			prop: "orderName",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "订单是否确认",
			prop: "isConfirmed",
			flex: false,
			component: { name: "cl-switch" },
			required: true
		},
		{
			label: "订单价格",
			prop: "orderPrice",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		}
	]
});

// cl-table
const Table = useTable({
	columns: [
		{ type: "selection" },
		{ label: "订单名称", prop: "orderName", minWidth: 140 },
		{
			label: "订单是否确认",
			prop: "isConfirmed",
			minWidth: 100,
			component: { name: "cl-switch" }
		},
		{ label: "订单价格", prop: "orderPrice", minWidth: 140 },
		{
			label: "创建时间",
			prop: "createTime",
			minWidth: 170,
			sortable: "custom",
			component: { name: "cl-date-text" }
		},
		{
			label: "更新时间",
			prop: "updateTime",
			minWidth: 170,
			sortable: "custom",
			component: { name: "cl-date-text" }
		},
		{ type: "op", buttons: ["edit", "delete"] }
	]
});

// cl-crud
const Crud = useCrud(
	{
		service: service.app.confirm
	},
	(app) => {
		app.refresh();
	}
);
</script>
