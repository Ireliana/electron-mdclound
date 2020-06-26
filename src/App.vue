<template>
    <div id="app">
        <el-row>
            <el-col :span="8" class="panel-left">
                <file-search />
                <file-list
                    :files="fileList"
                    :onSave="onSaveFilename"
                />
            </el-col>
            <el-col :span="16">
                <div>
                    dwqddqwdq
                </div>
            </el-col>
        </el-row>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from "vue-property-decorator";
    import FileSearch from "@/components/FileSearch/index.vue";
    import FileList from "@/components/FileList/index.vue";
    import fileList from "@/mock/fileList.js";

    @Component({
        components: {
            FileSearch,
            FileList
        }
    })
    export default class App extends Vue {
        fileList = fileList
        onSaveFilename(data:any) {
            for (let i = 0; i < fileList.length; i++) {
                if (fileList[i].id === data.id) {
                    fileList[i].title = data.title;
                }
            }
        }
    }
</script>

<style lang="less">
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        .panel-left {
            background: #f8f9fa;
            height: 100vh;
            min-width: 200px;
            max-width: 350px;
        }
    }
</style>
