<template>
    <div id="file-list">
        <ul>
            <li v-for="file in files" :key="file.id">
                <div class="title">
                    <i class="icon-md"></i>
                    <p v-show="editId !== file.id">{{ file.title }}</p>
                    <el-input
                        v-show="editId === file.id"
                        v-model="filename"
                        @keyup.enter.native="onSaveFilename"
                        @keyup.esc.native="onExit"
                        :ref="'input-' + file.id"
                    />
                </div>
                <div>
                    <i @click="onFileEdit(file)" class="el-icon-edit"></i
                    ><i @click="onDel(file)" class="el-icon-delete-solid"></i>
                </div>
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
    import { Component, Vue, Prop } from "vue-property-decorator";
    import { Input } from "element-ui";
    @Component
    export default class FileList extends Vue {
        @Prop({ type: Array, default: [] })
        files!: any[];
        @Prop({ type: Function, default: () => {} })
        onFileClick!: Function;
        @Prop({ type: Function, default: () => {} })
        onFileDelete!: Function;
        @Prop({ type: Function, default: () => {} })
        onSave!: Function;

        editId = -1;
        filename = "";
        onFileEdit(file: any) {
            this.editId = file.id;
            this.filename = file.title;
            let input = this.$refs[`input-${file.id}`] as any;
            this.$nextTick(() => {
                input && input[0].focus();
            });
        }
        onExit() {
            this.editId = -1;
        }
        onSaveFilename() {
            this.onSave({ id: this.editId, title: this.filename });
            this.editId = -1;
        }
        onDel(file: any) {
            console.log(file.id, file.title);
        }
    }
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
            .title {
                display: flex;
                align-items: center;
            }
            .icon-md {
                width: 1.5rem;
                height: 1.5rem;
                margin-right: 0.6rem;
                background: url("~@/assets/images/icon-md.png") no-repeat
                    center/100% 100%;
            }
        }
    }
</style>
