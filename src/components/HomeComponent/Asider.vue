<template>
    <div class="left-asider">
        <el-tabs v-model="activeName" :stretch="true">
            <el-tab-pane label="All" name="first">
                <AsiderSort></AsiderSort>
            </el-tab-pane>
            <el-tab-pane label="Outline" name="second">
                <AsiderOutline></AsiderOutline>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script>
    import AsiderOutline from "./Asider-Outline";
    import AsiderSort from "./Asider-Sort";
    export default {
        name: "Asider",
        components: {AsiderSort, AsiderOutline},
        data() {
            return {
                activeName: 'second'
            };
        },
    }
</script>

<style scoped>
    .left-asider{
        padding: 5% 10%;
        height: 80%;
    }
</style>