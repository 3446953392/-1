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

<script lang="ts" name="base-confirm" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "订单编号",
			prop: "orderNo",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "订单日期",
			prop: "orderDate",
			component: {
				name: "el-date-picker",
				props: { type: "date", valueFormat: "YYYY-MM-DD" }
			},
			required: true
		},
		{
			label: "用户姓名",
			prop: "userName",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "联系方式",
			prop: "contactInfo",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "时间表",
			prop: "timeTable",
			component: { name: "cl-editor-wang" },
			required: true
		},
		{
			label: "参加人数",
			prop: "participantCount",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "项目名称",
			prop: "projectName",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "总费用",
			prop: "totalFee",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "是否确认",
			prop: "isConfirmed",
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
		{ label: "订单编号", prop: "orderNo", minWidth: 140 },
		{
			label: "订单日期",
			prop: "orderDate",
			minWidth: 140,
			sortable: "custom",
			component: { name: "cl-date-text" }
		},
		{ label: "用户姓名", prop: "userName", minWidth: 140 },
		{ label: "联系方式", prop: "contactInfo", minWidth: 140 },
		{
			label: "时间表",
			prop: "timeTable",
			minWidth: 120,
			component: { name: "cl-editor-preview", props: { name: "wang" } }
		},
		{ label: "参加人数", prop: "participantCount", minWidth: 140 },
		{ label: "项目名称", prop: "projectName", minWidth: 140 },
		{ label: "总费用", prop: "totalFee", minWidth: 140 },
		{
			label: "是否确认",
			prop: "isConfirmed",
			minWidth: 100,
			component: { name: "cl-switch" }
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
		service: service.base.confirm
	},
	(app) => {
		app.refresh();
	}
);
</script>
