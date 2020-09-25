<template>
	<div id="file-list">
		<ul>
			<li v-for="file in files" :key="file.id">
				<div v-if="editId !== file.id" class="file-item">
					<FileMarkdownOutlined :style="iconMdStyle" />
					<div>{{ file.title }}</div>
				</div>
				<div v-else class="file-item">
					<a-input
						v-model="filename"
						@keyup.enter="onSaveFilename"
						@keyup.esc="onExit"
						:ref="'input-' + file.id"
						placeholder="请输入文件名称"
					/>
					<CloseOutlined @click="onDel(file)" />
				</div>
			</li>
		</ul>
	</div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import { FileMarkdownOutlined, CloseOutlined } from '@ant-design/icons-vue'

export default defineComponent({
	name: 'FileList',
	props: {
		files: {
			type: Array,
			required: true,
			default: () => [],
		},
		onFileClick: {
			type: Function,
		},
		onFileDelete: {
			type: Function,
		},
		onSave: {
			type: Function,
			required: true,
		},
	},
	setup() {
		const editId = ref(0)
		const filename = ref('')

		const iconMdStyle = computed(() => ({
			marginRight: '0.6rem',
			fontSize: '1.5rem',
		}))
		return {
			editId,
			filename,
			iconMdStyle,
		}
	},
	methods: {
		onFileEdit(file: any) {
			this.editId = file.id
			this.filename = file.title
			const input = this.$refs[`input-${file.id}`] as any
			this.$nextTick(() => {
				input && input[0].focus()
			})
		},
		onExit() {
			this.editId = -1
		},
		onSaveFilename() {
			this.onSave({ id: this.editId, title: this.filename })
			this.editId = -1
		},
		onDel(file: any) {
			console.log(file.id, file.title)
		},
	},
	components: {
		FileMarkdownOutlined,
		CloseOutlined,
	},
})
</script>

<style lang="less">
#file-list {
	li {
		position: relative;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 0.75rem 14%;
		background-color: #fff;
		&:not(:last-child) {
			border-bottom: 1px solid rgba(0, 0, 0, 0.125);
		}
		.file-item {
			width: 100%;
			display: flex;
			align-items: center;
		}
		.anticon-close {
			margin-left: 6px;
		}
	}
}
</style>
