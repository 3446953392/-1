<template>
	<cl-crud ref="Crud">
		<cl-row>
			<!-- 刷新按钮 -->
			<cl-refresh-btn />

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

<script lang="ts" name="recycle-data" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{ label: "表", prop: "entityInfo", component: { name: "cl-editor-wang" }, required: true },
		{ label: "操作人", prop: "userId", hook: "number", component: { name: "el-input-number" } },
		{
			label: "被删除的数据",
			prop: "data",
			component: { name: "cl-editor-wang" },
			required: true
		},
		{
			label: "请求的接口",
			prop: "url",
			component: { name: "el-input", props: { clearable: true } }
		},
		{ label: "请求参数", prop: "params", component: { name: "cl-editor-wang" } },
		{
			label: "删除数据条数",
			prop: "count",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		}
	]
});

// cl-table
const Table = useTable({
	columns: [
		{ label: "#", type: "index" },
		{
			label: "表",
			prop: "entityInfo",
			minWidth: 120,
			component: { name: "cl-editor-preview", props: { name: "wang" } }
		},
		{ label: "操作人", prop: "userId", minWidth: 140 },
		{
			label: "被删除的数据",
			prop: "data",
			minWidth: 120,
			component: { name: "cl-editor-preview", props: { name: "wang" } }
		},
		{ label: "请求的接口", prop: "url", minWidth: 140 },
		{
			label: "请求参数",
			prop: "params",
			minWidth: 120,
			component: { name: "cl-editor-preview", props: { name: "wang" } }
		},
		{ label: "删除数据条数", prop: "count", minWidth: 140 },
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
		}
	]
});

// cl-crud
const Crud = useCrud(
	{
		service: service.recycle.data
	},
	(app) => {
		app.refresh();
	}
);
</script>
