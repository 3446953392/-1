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

<script lang="ts" name="base-sys-user2" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "部门ID",
			prop: "departmentId",
			hook: "number",
			component: { name: "el-input-number" }
		},
		{
			label: "姓名",
			prop: "name",
			component: { name: "el-input", props: { clearable: true } }
		},
		{
			label: "用户名",
			prop: "username",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "密码",
			prop: "password",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "密码版本,",
			prop: "passwordV",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "昵称",
			prop: "nickName",
			component: { name: "el-input", props: { clearable: true } }
		},
		{ label: "头像", prop: "headImg", component: { name: "cl-upload" } },
		{
			label: "手机",
			prop: "phone",
			component: { name: "el-input", props: { clearable: true } }
		},
		{
			label: "邮箱",
			prop: "email",
			component: { name: "el-input", props: { clearable: true } }
		},
		{
			label: "备注",
			prop: "remark",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } }
		},
		{
			label: "状态",
			prop: "status",
			flex: false,
			component: { name: "cl-switch" },
			required: true
		},
		{
			label: "socketId",
			prop: "socketId",
			component: { name: "el-input", props: { clearable: true } }
		}
	]
});

// cl-table
const Table = useTable({
	columns: [
		{ type: "selection" },
		{ label: "部门ID", prop: "departmentId", minWidth: 140 },
		{ label: "姓名", prop: "name", minWidth: 140 },
		{ label: "用户名", prop: "username", minWidth: 140 },
		{ label: "密码", prop: "password", minWidth: 140 },
		{ label: "密码版本,", prop: "passwordV", minWidth: 140 },
		{ label: "昵称", prop: "nickName", minWidth: 140 },
		{
			label: "头像",
			prop: "headImg",
			minWidth: 100,
			component: { name: "cl-image", props: { size: 60 } }
		},
		{ label: "手机", prop: "phone", minWidth: 140 },
		{ label: "邮箱", prop: "email", minWidth: 140 },
		{ label: "备注", prop: "remark", showOverflowTooltip: true, minWidth: 200 },
		{ label: "状态", prop: "status", minWidth: 100, component: { name: "cl-switch" } },
		{ label: "socketId", prop: "socketId", minWidth: 140 },
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
		service: service.base.sys.user
	},
	(app) => {
		app.refresh();
	}
);
</script>
