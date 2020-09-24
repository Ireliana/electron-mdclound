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
    import { Component, Vue, Prop } from "vue-property-decorator";
    @Component
    export default class TabList extends Vue {
        @Prop({ type: Array, default: [] })
        files!: any[];
        @Prop({ type: Number, default: "" })
        activeId!: number;
        @Prop({ type: Array, default: () => [] })
        unSaveIds!: any[];
        @Prop({ type: Function, default: () => {} })
        onClick!: Function;
        @Prop({ type: Function, default: () => {} })
        onClose!: Function;

        get fileStatusClass() {
            return "el-icon-close";
        }
        isUnSave(id: any) {
            return this.unSaveIds.includes(id);
        }
    }
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
