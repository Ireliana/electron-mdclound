<template>
	<div id="app">
		<a-row>
			<a-col :span="8" class="panel-left">
				<file-search />
				<file-list :files="fileList" :onSave="onSaveFilename" />
				<div class="btn-group">
					<div class="btn btn-add">
						<PlusOutlined class="icon-btn" />
						新建
					</div>
					<div class="btn btn-import">
						<FolderAddOutlined class="icon-btn" />
						<i></i>
						导入
					</div>
				</div>
			</a-col>
			<a-col :span="16">
				<TabList
					:files="fileList"
					:activeId="1"
					:onClick="onTabListClick"
					:onClose="onTabListClose"
					:unSaveIds="['1']"
				/>
			</a-col>
		</a-row>
	</div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue'
import FileSearch from '@/components/FileSearch/index.vue'
import FileList from '@/components/FileList/index.vue'
import fileList from '@/mock/fileList.ts'
import TabList from '@/components/TabList/index.vue'
import { PlusOutlined, FolderAddOutlined } from '@ant-design/icons-vue'

export default defineComponent({
	name: 'App',
	setup() {
		return {
			fileList: reactive(fileList),
		}
	},
	onSaveFilename(data: any) {
		for (let i = 0; i < fileList.length; i++) {
			if (fileList[i].id === data.id) {
				fileList[i].title = data.title
			}
		}
	},
	onTabListClick(id: number) {
		console.log(id)
	},
	onTabListClose(id: number) {
		console.log('close', id)
	},
	components: {
		FileSearch,
		FileList,
		TabList,
		PlusOutlined,
		FolderAddOutlined,
	}
})
</script>

<style lang="less">
#app {
	.panel-left {
		position: relative;
		background: #f8f9fa;
		height: 100vh;
		min-width: 200px;
		max-width: 350px;
	}
	.btn-group {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;
		display: flex;
		.btn {
			display: flex;
			flex: 1;
			align-items: center;
			justify-content: center;
			color: #fff;
			padding: 10px 0;
			cursor: pointer;
		}
		span[role='img'] {
			margin-right: 2px;
		}
		.btn-add {
			background-color: #007bff;
		}
		.btn-import {
			background-color: #28a745;
		}
	}
}
</style>
