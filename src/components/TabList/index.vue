<template>
	<div id="tab-list">
		<ul>
			<li
				:class="{ active: activeId == file.id }"
				v-for="file in files"
				:key="file.id"
				@click="onClick(file.id)"
			>
				<span>
					{{ file.title }}
				</span>
				<div class="icon-wrapper">
					<i v-show="isUnSave(file.id)" class="icon-circle"></i>
					<i
						v-show="!isUnSave(file.id)"
						class="el-icon-close"
						@click.stop="onClose(file.id)"
					></i>
				</div>
			</li>
		</ul>
	</div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue'
export default defineComponent({
	name: 'TabList',
	props: {
		files: {
			type: Array,
			defalut: () => [],
		},
		activeId: {
			type: Number,
			defalut: 0,
		},
		unSaveIds: {
			type: Array,
			required: true,
			defalut: () => [],
		},
		onClick: {
			type: Function,
		},
		onClose: {
			type: Function,
		},
	},
	setup() {
		const fileStatusClass = computed(() => {
			return 'el-icon-close'
		})
		return {
			fileStatusClass,
		}
	},
	methods: {
		isUnSave(id: any) {
			return this.unSaveIds.includes(id)
		},
	},
})
</script>

<style lang="less">
#tab-list {
	ul {
		display: flex;
	}
	li {
		padding: 4px 8px;
		border-radius: 4px;
		color: #007bff;
		cursor: pointer;
		display: flex;
		align-items: center;
		&.active {
			background: #007bff;
			color: #fff;
		}
		&:hover,
		&.active {
			i {
				opacity: 1;
			}
		}
		i {
			opacity: 0;
			margin-left: 4px;
		}
		.icon-wrapper:hover {
			.icon-circle {
				width: 0;
			}
		}
		.icon-circle {
			width: 8px;
			height: 8px;
			border-radius: 50%;
			background: #eee;
			margin-left: 8px;
		}
	}
}
</style>
