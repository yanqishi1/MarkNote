<template>
    <el-menu
            default-active="2"
            class="el-menu-sort"
            background-color="#fafafa"
            @open="handleOpen"
            @close="handleClose">
        <el-submenu index="1">
            <template slot="title">
                <i class="el-icon-grape"></i>
                <span>Classification</span>
            </template>
            <el-submenu index="1-1">
                <template slot="title">Study</template>
                <el-menu-item index="1-1-1">item1</el-menu-item>
                <el-menu-item index="1-1-2">item2</el-menu-item>
                <el-menu-item index="1-1-3">item3</el-menu-item>
                <el-submenu index="1-1-4">
                    <template slot="title">Class1-4</template>
                    <el-menu-item index="1-1-4-1">item1</el-menu-item>
                    <el-menu-item index="1-1-4-2">item2</el-menu-item>
                    <el-menu-item index="1-1-4-3">item3</el-menu-item>
                </el-submenu>
            </el-submenu>
            <el-submenu index="1-2">
                <template slot="title">Work</template>
                <el-menu-item index="1-2-1">item1</el-menu-item>
            </el-submenu>
        </el-submenu>
        <el-menu-item index="2">
            <i class="el-icon-star-off"></i>
            <span slot="title">Star</span>
        </el-menu-item>
        <el-menu-item index="3">
            <i class="el-icon-document"></i>
            <span slot="title">Drafts</span>
        </el-menu-item>
    </el-menu>
</template>

<script>
    export default {
        name: "Asider-Sort",
        methods: {
            handleOpen(key, keyPath) {
                console.log(key, keyPath);
            },
            handleClose(key, keyPath) {
                console.log(key, keyPath);
            }
        }
    }
</script>

<style scoped>
    .el-menu-sort{
        border:none;
    }
</style>