<template>
    <div class="home-footer">
        <div class="home-footer-content">
            <el-tooltip class="item" effect="light" content="Hide and Show Asider" placement="top">
                <i @click="sider" :class="arrow_dir"></i>
            </el-tooltip>
            <el-tooltip class="item" effect="light" content="Code Mode" placement="top">
                <i @click="codeMode" class="el-icon-view"></i>
            </el-tooltip>
            <el-tooltip class="item" effect="light" content="Statistical" placement="top">
                <i class="home-footer-content-word">{{$store.state.words.word}} words   {{$store.state.words.character}} Charaters</i>
            </el-tooltip>
        </div>
    </div>
</template>

<script>
    export default {
        props:['words'],
        name: "HomeFooter",
        data(){
          return {
              arrow_dir:'el-icon-arrow-left'
          }
        },
        methods:{
            sider(){
                this.$emit("show_hide_asider")
                if(this.arrow_dir=='el-icon-arrow-left'){
                    this.arrow_dir='el-icon-arrow-right'
                }else {
                    this.arrow_dir='el-icon-arrow-left'
                }

            },
            codeMode(){

            }
        }
    }
</script>

<style scoped>
    .home-footer-content{

    }
    .home-footer-content i{
        padding: 5px 10px 0px 10px;
    }
    .home-footer-content i:hover{
        background: #fafafa;
    }
    .home-footer-content-word{
        /*float: right;*/
        font-size: 10px;
        font-style: normal;
        color: grey;
        padding:0 20px;
        margin-right: 20px;
    }
</style>