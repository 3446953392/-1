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

<script lang="ts" name="dict-activity" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "活动ID",
			prop: "activityId",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "研学活动的名称",
			prop: "name",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "活动的简要描述",
			prop: "description",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } }
		},
		{
			label: "活动地点",
			prop: "location",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "时间范围",
			prop: "time",
			component: {
				name: "el-date-picker",
				props: {
					type: "datetimerange",
					valueFormat: "YYYY-MM-DD HH:mm:ss",
					defaultTime: ["2000-01-31T16:00:00.000Z", "2000-02-01T15:59:59.000Z"]
				}
			},
			required: true,
			hook: "datetimeRange"
		},
		{
			label: "最大参与人数",
			prop: "maxParticipants",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "已报名人数",
			prop: "currentParticipants",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "活动状态",
			prop: "status",
			component: { name: "el-radio-group", options: [] },
			required: true
		}
	]
});

// cl-table
const Table = useTable({
	columns: [
		{ type: "selection" },
		{ label: "活动ID", prop: "activityId", minWidth: 140 },
		{ label: "研学活动的名称", prop: "name", minWidth: 140 },
		{ label: "活动的简要描述", prop: "description", showOverflowTooltip: true, minWidth: 200 },
		{ label: "活动地点", prop: "location", minWidth: 140 },
		{
			label: "活动开始的日期和时间",
			prop: "startTime",
			minWidth: 170,
			sortable: "custom",
			component: { name: "cl-date-text" }
		},
		{
			label: "活动结束的日期和时间",
			prop: "endTime",
			minWidth: 170,
			sortable: "custom",
			component: { name: "cl-date-text" }
		},
		{ label: "最大参与人数", prop: "maxParticipants", minWidth: 140 },
		{ label: "已报名人数", prop: "currentParticipants", minWidth: 140 },
		{ label: "活动状态", prop: "status", dict: [], dictColor: true, minWidth: 120 },
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
		service: service.dict.activity
	},
	(app) => {
		app.refresh();
	}
);
</script>
