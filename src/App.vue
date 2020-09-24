<template>
    <div id="app">
        <el-row>
            <el-col :span="8" class="panel-left">
                <file-search />
                <file-list :files="fileList" :onSave="onSaveFilename" />
                <div class="btn-group">
                    <div class="btn btn-add">
                        <i class="el-icon-plus"></i>
                        新建
                    </div>
                    <div class="btn btn-import">
                        <i class="el-icon-folder-add"></i>
                        导入
                    </div>
                </div>
            </el-col>
            <el-col :span="16">
                <TabList
                    :files="fileList"
                    :activeId="1"
                    :onClick="onTabListClick"
                    :onClose="onTabListClose"
                    :unSaveIds="['1']"
                />
            </el-col>
        </el-row>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from "vue-property-decorator";
    import FileSearch from "@/components/FileSearch/index.vue";
    import FileList from "@/components/FileList/index.vue";
    import fileList from "@/mock/fileList.ts";
    import TabList from "@/components/TabList/index.vue";

    @Component({
        components: {
            FileSearch,
            FileList,
            TabList
        }
    })
    export default class App extends Vue {
        fileList = fileList;
        onSaveFilename(data: any) {
            for (let i = 0; i < fileList.length; i++) {
                if (fileList[i].id === data.id) {
                    fileList[i].title = data.title;
                }
            }
        }
        onTabListClick(id: number) {
            console.log(id);
        }
        onTabListClose(id: number) {
            console.log("close", id);
        }
    }
</script>

<style lang="less">
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
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
            i {
                margin-left: 4px;
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
