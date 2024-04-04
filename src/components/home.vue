<template>
    <v-container>
        <v-row>
            <h1>Home</h1>
        </v-row>

        <v-row style="margin-top: 34px;">
            <v-divider></v-divider>
        </v-row>

        <v-row style="margin-top: 30px;">
            <p>Start a new project:</p>
        </v-row>

        <v-row style="margin-top: 15px;">
            <u>Start from empty</u>
        </v-row>

        <v-row style="margin-top: 15px;">
            <u @click="openDialog()">Start from a JSON file</u>
        </v-row>

        <v-row style="margin-top: 30px;">
            <v-divider></v-divider>
        </v-row>

        <v-row style="margin-top: 30px;">
            <p>Recent project:</p>
        </v-row>

        <v-row></v-row>
    </v-container>

    <v-dialog v-model="dialog" max-width="500px">
        <template>
            <u @click="openDialog" style="cursor: pointer;">Upload JSON</u>
        </template>
        <v-card>
            <v-card-title>Upload JSON File</v-card-title>
            <v-card-text>
                <!-- 添加文件上传组件 -->
                <v-file-input v-model="file" label="Choose a JSON file" accept=".json"></v-file-input>
            </v-card-text>
            <v-card-actions>
                <v-btn color="primary" @click="uploadFile">Upload</v-btn>
                <v-btn @click="dialog = false">Close</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
import { inject } from 'vue';

export default {
    name: 'homeTab',

    data() {
        return {
            dialog: false,
            file: null,
        };
    },
    methods: {
        openDialog() {
            this.dialog = true;
        },

        uploadFile() {
            if (this.file) {
                this.loadInfoData(this.file[0]);
                this.dialog = false;
            }
        },
    },

    setup() {
        const loadInfoData = inject('loadInfoData');

        return { loadInfoData };
    }
}
</script>

<style scoped>
h1 {
    font-size: 56px;
}
</style>