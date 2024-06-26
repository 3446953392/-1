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

<script lang="ts" name="base-schedule" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "资源名称",
			prop: "resourceName",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "资源花费",
			prop: "resourceCost",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "资源时间",
			prop: "resourceTime",
			component: {
				name: "el-date-picker",
				props: { type: "datetime", valueFormat: "YYYY-MM-DD HH:mm:ss" }
			},
			required: true
		},
		{
			label: "资源使用人数",
			prop: "resourceUsers",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "联系方式",
			prop: "contact",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		}
	]
});

// cl-table
const Table = useTable({
	columns: [
		{ type: "selection" },
		{ label: "资源名称", prop: "resourceName", minWidth: 140 },
		{ label: "资源花费", prop: "resourceCost", minWidth: 140 },
		{
			label: "资源时间",
			prop: "resourceTime",
			minWidth: 170,
			sortable: "custom",
			component: { name: "cl-date-text" }
		},
		{ label: "资源使用人数", prop: "resourceUsers", minWidth: 140 },
		{ label: "联系方式", prop: "contact", minWidth: 140 },
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
		service: service.base.schedule
	},
	(app) => {
		app.refresh();
	}
);
</script>
