<template>
    <div>
        <div ref="editor"></div>
    </div>
</template>

<script>
    import Muya from '../../muya/lib'
    import TablePicker from '../../muya/lib/ui/tablePicker'
    import QuickInsert from '../../muya/lib/ui/quickInsert'
    import CodePicker from '../../muya/lib/ui/codePicker'
    import EmojiPicker from '../../muya/lib/ui/emojiPicker'
    import ImagePathPicker from '../../muya/lib/ui/imagePicker'
    import ImageSelector from '../../muya/lib/ui/imageSelector'
    import FormatPicker from '../../muya/lib/ui/formatPicker'
    import FrontMenu from '../../muya/lib/ui/frontMenu'
    import '../../muya/themes/default.css'
    import '../../assets/index.css'

    export default {
        name: 'HomeEditor',
        created () {
            this.$nextTick(() => {
                const ele = this.$refs.editor
                Muya.use(TablePicker)
                Muya.use(QuickInsert)
                Muya.use(CodePicker)
                Muya.use(EmojiPicker)
                Muya.use(ImagePathPicker)
                Muya.use(ImageSelector)
                Muya.use(FormatPicker)
                Muya.use(FrontMenu)

                this.editor = new Muya(ele, {
                    markdown: ''
                })
                this.editor.on('change', changes => {
                    console.log(changes)
                    this.$store.state.words = changes.wordCount

                    this.$store.state.toc = this.tocConvertData(changes.toc)
                })

                this.$store.state.editor = this.editor
            })
        },
        mounted() {
            var _this = this
            document.addEventListener('keydown',this.handleEvent)
            document.onkeydown = function(event) {
                if (event.ctrlKey == true && event.keyCode == 83) {//Ctrl+S
                    event.preventDefault();
                    event.returnValue = false;
                    _this.save()
                    return false;
                }

                if (event.ctrlKey == true && event.keyCode == 90) {//Ctrl+Z
                    event.returnvalue = false;
                    _this.undo()
                }

                if (event.ctrlKey == true && event.keyCode == 89) {//Ctrl+Y
                    event.returnvalue = false;
                    _this.redo()
                }

                if (event.ctrlKey == true && event.keyCode == 65) {//Ctrl+A
                    event.returnvalue = false;
                    _this.editor.selectAll()
                }

                if (event.ctrlKey == true && event.keyCode == 79) {//Ctrl+N
                    event.returnvalue = false;
                    window.location.href = "SetInfo.aspx?ChId=1&ColId=1"; //ID
                }
            }
        },
        methods:{
            tocConvertData(tocs){
                if(tocs.length==0){
                    return []
                }

                var tree=[]
                var data = []
                for(let i =0;i<7;i++){
                    data.push(null)
                }

                for(let i=0;i<tocs.length;i++){
                    var toc = tocs[i]
                    data[toc.lvl] = this.TOC(toc.content,toc.lvl,toc.slug,[])

                    //寻找直系父节点
                    for(let i=toc.lvl-1 ; i>0 ;i--){
                        if(data[i] != null && data[i].id<toc.lvl){
                            data[i].children.push(data[toc.lvl])
                            break
                        }
                    }

                    if(toc.lvl==1){
                        //如果是一级标题，加入tree中
                        tree.push(data[toc.lvl])
                    }else if(i==0 && toc.lvl>1){
                        //如果不是一级标题，并且没有找到直系父节点
                        //手动创建一个一级标题，并将此标题加入其中
                        let parent = this.TOC('',1,'',[data[toc.lvl]])
                        tree.push(parent)
                    }

                    //清除下面的子节点
                    for(let i=toc.lvl+1;i<7;i++){
                        if(data[i]!=null){
                            data[i] = null
                        }
                    }
                }
                console.log(tree);
                return tree
            },
            TOC(label,id,slug,child){
               return {label:label,id:id,slug:slug,children:child}
            },
            undo(){
                this.editor.undo()
            },
            redo(){
                this.editor.redo()
            },
            getWords(){
                this.$store.state.words = this.editor.getWordCount(this.editor.getMarkdown())
            },
            save(){
                console.log(this.editor.getMarkdown())
            },
        }
    }
</script>

<style>

</style>
