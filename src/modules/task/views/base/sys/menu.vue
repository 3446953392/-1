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

<script lang="ts" name="base-sys-menu" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "父菜单ID",
			prop: "parentId",
			hook: "number",
			component: { name: "el-input-number" }
		},
		{
			label: "菜单名称",
			prop: "name",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "菜单地址",
			prop: "router",
			component: { name: "el-input", props: { clearable: true } }
		},
		{
			label: "权限标识",
			prop: "perms",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } }
		},
		{
			label: "类型",
			prop: "type",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "图标",
			prop: "icon",
			component: { name: "el-input", props: { clearable: true } }
		},
		{
			label: "排序",
			prop: "orderNum",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "视图地址",
			prop: "viewPath",
			component: { name: "el-input", props: { clearable: true } }
		},
		{
			label: "路由缓存",
			prop: "keepAlive",
			flex: false,
			component: { name: "cl-switch" },
			required: true
		},
		{
			label: "是否显示",
			prop: "isShow",
			flex: false,
			component: { name: "cl-switch" },
			required: true
		}
	]
});

// cl-table
const Table = useTable({
	columns: [
		{ type: "selection" },
		{ label: "父菜单ID", prop: "parentId", minWidth: 140 },
		{ label: "菜单名称", prop: "name", minWidth: 140 },
		{ label: "菜单地址", prop: "router", minWidth: 140 },
		{ label: "权限标识", prop: "perms", showOverflowTooltip: true, minWidth: 200 },
		{ label: "类型", prop: "type", minWidth: 140 },
		{ label: "图标", prop: "icon", minWidth: 140 },
		{ label: "排序", prop: "orderNum", minWidth: 140 },
		{ label: "视图地址", prop: "viewPath", minWidth: 140 },
		{ label: "路由缓存", prop: "keepAlive", minWidth: 100, component: { name: "cl-switch" } },
		{ label: "是否显示", prop: "isShow", minWidth: 100, component: { name: "cl-switch" } },
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
		service: service.base.sys.menu
	},
	(app) => {
		app.refresh();
	}
);
</script>
