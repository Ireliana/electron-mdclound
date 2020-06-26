<template>
    <div id="file-search">
        <el-row>
            <el-col class="title" :span="14">
                <el-input
                    v-if="isSearch"
                    ref="file-input"
                    size="small"
                    v-model="filename"
                    @keyup.enter.native="onConfirm"
                    @keyup.esc.native="onExit"
                    placeholder="请输入文件名"
                ></el-input>
                <p v-else>
                    {{ title }}
                </p>
            </el-col>
            <el-col :span="6">
                <el-button @click="onSearch" type="small" :icon="iconName">{{
                    btnText
                }}</el-button>
            </el-col>
        </el-row>
    </div>
</template>

<script lang="ts">
    import { Component, Vue, Prop } from "vue-property-decorator";
    import { Input } from "element-ui";
    @Component({
        components: {}
    })
    export default class FileSearch extends Vue {
        @Prop({ type: String, default: "我的云文档" })
        title!: string;
        @Prop({ type: Function })
        onFileSearch!: Function;

        isSearch: boolean = false;
        filename: string = "";
        get btnText() {
            return !this.isSearch ? "搜索" : "关闭";
        }
        get iconName() {
            return !this.isSearch ? "el-icon-search" : "el-icon-close";
        }
        async onSearch() {
            this.isSearch = !this.isSearch;
            await this.$nextTick();
            if (this.isSearch) {
                (this.$refs["file-input"] as Input).focus();
            } else {
                this.filename = "";
            }
        }
        onConfirm() {
            console.log(this.filename);
        }
        onExit() {
            this.filename = "";
            this.isSearch = false;
        }
    }
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
    }
</style>
