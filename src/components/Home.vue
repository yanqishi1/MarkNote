<template>
    <div class="home">
        <el-container>
            <el-header style="padding: 0">
                <home-header></home-header>
            </el-header>
            <el-container>
                <el-aside v-show="asider">
                    <asider></asider>
                </el-aside>
                <el-container>
                    <el-main>
                        <home-editor></home-editor>
                    </el-main>
                    <el-footer style="height: 30px;padding: 0px">
                       <home-footer :words="20" @show_hide_asider="show_hide_asider"></home-footer>
                    </el-footer>
                </el-container>
            </el-container>
        </el-container>
    </div>
</template>

<script>
    import Asider from "@/components/HomeComponent/Asider";
    import HomeFooter from "@/components/HomeComponent/HomeFooter";
    import HomeHeader from "@/components/HomeComponent/HomeHeader";
    import HomeEditor from "@/components/HomeComponent/HomeEditor";
    export default {
        name: "Home",
        components: {
            Asider,
            HomeEditor,
            HomeFooter,
            HomeHeader
        },
        data(){
          return{
              asider:true,
          }
        },
        methods:{
            show_hide_asider(){
                this.asider=!this.asider;
            }
        }
    }
</script>

<style scoped>
    .home{
        height: 100%;
    }
    .el-container{
        height: 100%;
    }
    .el-aside{
        background: #fafafa;
    }
    .el-footer{
        border-top: solid 1px gainsboro ;
        position: fixed;
        bottom: 0;
        width: 100%;
    }
</style>