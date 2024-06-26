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

<script lang="ts" name="demo-goods" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "标题",
			prop: "title",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "价格",
			prop: "price",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "描述",
			prop: "description",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } }
		},
		{ label: "主图", prop: "mainImage", component: { name: "cl-upload" } },
		{
			label: "示例图",
			prop: "exampleImages",
			component: { name: "cl-upload", props: { multiple: true } }
		},
		{
			label: "库存",
			prop: "stock",
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
		{ label: "标题", prop: "title", minWidth: 140 },
		{ label: "价格", prop: "price", minWidth: 140 },
		{ label: "描述", prop: "description", showOverflowTooltip: true, minWidth: 200 },
		{
			label: "主图",
			prop: "mainImage",
			minWidth: 100,
			component: { name: "cl-image", props: { size: 60 } }
		},
		{
			label: "示例图",
			prop: "exampleImages",
			minWidth: 100,
			component: { name: "cl-image", props: { size: 60 } }
		},
		{ label: "库存", prop: "stock", minWidth: 140 },
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
		service: service.demo.goods
	},
	(app) => {
		app.refresh();
	}
);
</script>
