<template>
    <div class="home-header">
        <input id="localfile" type='file' ref="refFile" v-on:change="openFile" hidden>
        <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal">
            <el-submenu index="1">
                <template slot="title">WorkStation</template>
                <el-menu-item index="2-1">Save</el-menu-item>
                <el-menu-item index="2-2" @click="clickbutton">Import</el-menu-item>
                <el-menu-item index="2-4" @click="ExportData">Export</el-menu-item>
            </el-submenu>
            <el-menu-item index="2">Edit</el-menu-item>
            <el-menu-item index="3">Help</el-menu-item>
        </el-menu>
        <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal">
            <el-menu-item index="1" @click="input_setFocus">
                <input class="title_input" v-model="title"
                       v-show="title_input"
                       @blur="input_setBlur"
                       @keyup.enter="input_setBlur"/>
                <span class="mark-title"
                      v-show="title_input == false"
                      @click="input_setFocus">{{title}}</span>
            </el-menu-item>
            <el-menu-item index="2">
                <el-select
                        v-model="value"
                        multiple
                        filterable
                        allow-create
                        default-first-option
                        placeholder="Please set tag">
                    <el-option
                            v-for="tag in tags"
                            :key="tag.value"
                            :label="tag.label"
                            :value="tag.value">
                    </el-option>
                </el-select>
            </el-menu-item>
            <el-menu-item index="3" @click="set_star"><i id="star" :class="star_class"></i></el-menu-item>
        </el-menu>
    </div>
</template>

<script>
    export default {
        name: "Home-header",
        data() {
            return {
                tags:[{
                    value:'work',
                    label:'work'
                },{
                    value:'study',
                    label:'study'
                }],
                value: [],
                title:'untitled',
                activeIndex: "1",
                title_input:false,
                star_class:'el-icon-star-off'
            }
        },
        methods:{
            set_star(){
                if("el-icon-star-off" == this.star_class){
                    this.star_class = "el-icon-star-on"
                }else{
                    this.star_class = "el-icon-star-off"
                }
            },
            input_setFocus(){
                this.title_input = true
            },
            input_setBlur(){
                this.title_input = false
            },
            ExportData(){
                var data = this.$store.state.editor.getMarkdown()
                if (!data) {
                    return
                }
                let blob = new Blob([data], {type: 'application/md'})
                let url = window.URL.createObjectURL(blob)
                let link = document.createElement('a')
                link.style.display = 'none'
                link.href = url
                link.download=this.title+'.md'
                document.body.appendChild(link)
                link.click()
            },
            clickbutton(){
                document.getElementById("localfile").click()
            },
            openFile(){
                const selectedFile = this.$refs.refFile.files[0];
                var reader = new FileReader();
                reader.readAsText(selectedFile);

                var _this = this
                reader.onload = function() {
                    console.log(this.result);
                    _this.$store.state.editor.setMarkdown(this.result);
                    _this.title = selectedFile.name.split('.')[0]
                }
            }
        }
    }
</script>

<style scoped>
    .home-header{
        display: flex;
        justify-content: space-between;
        border-bottom: solid 1px #e6e6e6;
    }
    .el-dropdown-link {
        cursor: pointer;
        color: #409EFF;
    }
    .el-icon-arrow-down {
        font-size: 12px;
    }
    .title_input{
        font-size: 16px;
        border: none;
        outline: none;
        width: 80%;
    }
</style>