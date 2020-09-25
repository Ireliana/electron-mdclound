<template>
	<div id="file-search">
		<a-row>
			<a-col class="title" :span="14">
				<a-input
                    v-if="isSearch"
                    ref="file-input"
                    size="small"
                    v-model="filename"
                    @keyup.enter="onConfirm"
                    @keyup.esc="onExit"
                    placeholder="请输入文件名"
                ></a-input>
                <div v-else>
                    {{ title }}
                </div>
			</a-col>
			<a-col :span="6">
				<a-button type="link" @click="onSearch" shape="round" size="small">
					<template v-slot:icon>
						<component :is="iconName"></component>
						{{ btnText }}
					</template>
				</a-button>
			</a-col>
		</a-row>
	</div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import { SearchOutlined, CloseOutlined } from '@ant-design/icons-vue'

export default defineComponent({
	name: 'FileSearch',
	props: {
		title: {
			type: String,
			default: '我的云文档',
		},
		onFileSearch: {
			type: Function,
			required: true,
		},
	},
	setup() {
		const isSearch = ref(false)
		const filename = ref('')
		const btnText = computed(() => {
			return !isSearch.value ? '搜索' : '关闭'
		})

		const iconName = computed(() => {
			return !isSearch.value ? 'SearchOutlined' : 'CloseOutlined'
		})
		return {
			isSearch,
			filename,
			btnText,
			iconName,
		}
	},
	methods: {
		async onSearch() {
			this.isSearch = !this.isSearch
			await this.$nextTick()
			if (this.isSearch) {
				(this.$refs['file-input'] as HTMLInputElement).focus()
			} else {
				this.filename = ''
			}
		},
		onConfirm() {
			console.log(this.filename)
		},
		onExit() {
			this.filename = ''
			this.isSearch = false
		},
	},
	components: {
		SearchOutlined,
		CloseOutlined,
	},
})
</script>

<style lang="less">
#file-search {
	padding: 0.75rem 1.25rem;
	background-color: #cce5ff;
	border-color: #b8daff;
	.el-row {
		display: flex;
		align-items: center;
		text-align: center;
	}
	.el-button {
		border: none;
		background: transparent;
		&:focus {
			color: #606266;
		}
		&:hover {
			color: #409eff;
		}
    }
    .title{
        text-align: center;
    }
}
</style>
