<template>
    <div id="app">
        <el-row>
            <el-col :span="6">
                <file-search/>
            </el-col>
            <el-col :span="18">
                <div>
                    dwqddqwdq
                </div>
            </el-col>
        </el-row>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from "vue-property-decorator";
    import FileSearch from "@/components/FileSearch/index.vue"
    @Component({
        components: {
            FileSearch
        }
    })
    export default class App extends Vue {}
</script>

<style lang="less">
    * {
        padding: 0;
        margin: 0;
    }
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        
    }
</style>
