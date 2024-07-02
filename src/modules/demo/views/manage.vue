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

<script lang="ts" name="demo-manage" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert
const Upsert = useUpsert({
	items: [
		{
			label: "名称",
			prop: "name",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "报名数",
			prop: "signupCount",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "简介",
			prop: "summary",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } }
		},
		{
			label: "地点",
			prop: "location",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "时间",
			prop: "time",
			component: {
				name: "el-date-picker",
				props: { type: "datetime", valueFormat: "YYYY-MM-DD HH:mm:ss" }
			},
			required: true
		},
		{
			label: "基地介绍",
			prop: "baseIntroduction",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } },
			required: true
		},
		{
			label: "研学流程",
			prop: "studyProcess",
			component: { name: "el-input", props: { type: "textarea", rows: 4 } },
			required: true
		},
		{
			label: "餐饮名称",
			prop: "cateringName",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "餐饮地址",
			prop: "cateringAddress",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "住宿名称",
			prop: "accommodationName",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "住宿地址",
			prop: "accommodationAddress",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{
			label: "文创名称",
			prop: "culturalCreativeName",
			component: { name: "el-input", props: { clearable: true } },
			required: true
		},
		{ label: "文创图片", prop: "culturalCreativeImage", component: { name: "cl-upload" } },
		{
			label: "基地位置-经度",
			prop: "longitude",
			hook: "number",
			component: { name: "el-input-number" },
			required: true
		},
		{
			label: "基地位置-纬度",
			prop: "latitude",
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
		{ label: "名称", prop: "name", minWidth: 140 },
		{ label: "报名数", prop: "signupCount", minWidth: 140 },
		{ label: "简介", prop: "summary", showOverflowTooltip: true, minWidth: 200 },
		{ label: "地点", prop: "location", minWidth: 140 },
		{
			label: "时间",
			prop: "time",
			minWidth: 170,
			sortable: "custom",
			component: { name: "cl-date-text" }
		},
		{
			label: "基地介绍",
			prop: "baseIntroduction",
			showOverflowTooltip: true,
			minWidth: 200
		},
		{ label: "研学流程", prop: "studyProcess", showOverflowTooltip: true, minWidth: 200 },
		{ label: "餐饮名称", prop: "cateringName", minWidth: 140 },
		{ label: "餐饮地址", prop: "cateringAddress", minWidth: 140 },
		{ label: "住宿名称", prop: "accommodationName", minWidth: 140 },
		{ label: "住宿地址", prop: "accommodationAddress", minWidth: 140 },
		{ label: "文创名称", prop: "culturalCreativeName", minWidth: 140 },
		{
			label: "文创图片",
			prop: "culturalCreativeImage",
			minWidth: 100,
			component: { name: "cl-image", props: { size: 60 } }
		},
		{ label: "基地位置-经度", prop: "longitude", minWidth: 140 },
		{ label: "基地位置-纬度", prop: "latitude", minWidth: 140 },
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
		service: service.demo.manage
	},
	(app) => {
		app.refresh();
	}
);
</script>
