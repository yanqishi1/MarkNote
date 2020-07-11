<template>
    <el-tree
            class="outline-tree"
            :data="$store.state.toc"
            :props="defaultProps"
            @node-click="handleNodeClick"></el-tree>
</template>

<script>
    export default {
        name: "Asider-Outline",
        data() {
            return {
                data: [{
                    label: '',
                    id:"ag-76",
                    children: [{
                        label: '二级 1-1',
                        children: [{
                            label: '三级 1-1-1'
                        }]
                    }]
                }],
                defaultProps: {
                    children: 'children',
                    label: 'label'
                }
            };
        },
        methods: {
            handleNodeClick(data) {
                console.log(data);
                document.querySelector("#"+data.slug).scrollIntoView();
            },

        }
    }
</script>

<style scoped>
    .outline-tree{
        background: #fafafa;
    }
</style>