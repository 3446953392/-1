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

<script lang="ts" name="theme-info" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "基地名称",
			prop: "name",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "省市区",
			prop: "pca",
			hook: "pca",
			component: { name: "cl-distpicker" },
			required: true
		},
		{
			label: "简介",
			prop: "summary",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } }
		},
		{
			label: "特色内容",
			prop: "featureContent",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } }
		},
		{ label: "图片", prop: "images", component: { name: "cl-upload" } }
	]
});

// cl-table
const Table = useTable({
	columns: [
		{ type: "selection" },
		{ label: "基地名称", prop: "name", minWidth: 140 },
		{
			label: "省市区",
			prop: "province",
			minWidth: 160,
			formatter(row) {
				return row.province + "-" + row.city + "-" + row.district;
			}
		},
		{ label: "简介", prop: "summary", showOverflowTooltip: true, minWidth: 200 },
		{ label: "特色内容", prop: "featureContent", showOverflowTooltip: true, minWidth: 200 },
		{
			label: "图片",
			prop: "images",
			minWidth: 100,
			component: { name: "cl-image", props: { size: 60 } }
		},
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
		service: service.theme.info
	},
	(app) => {
		app.refresh();
	}
);
</script>
