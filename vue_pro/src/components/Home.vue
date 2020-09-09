<template>
    <div>
        <input type="text" v-model="msg" ><input type="button" value="发表留言" @click="change_message">
        <br>
        <ul v-for="(value,index) in notebook">
            <li>{{value}} <a href="javascript:;" @click="del_message(index)">删除</a></li>
        </ul>
        <ul>
            <li>留言总数量：{{notebook.length}}<a href="javascript:;" @click="del_all" v-show="show">删除全部</a></li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "Home",
        data: function () {
            return {
                show:true,
                msg:"",
                message: [],
                notebook:localStorage.notebook ? JSON.parse(localStorage.notebook):[]
            }
        },
        methods: {
            change_message() {
                this.message.unshift(this.msg);
                localStorage.notebook = JSON.stringify(this.message);
                this.notebook= JSON.parse(localStorage.notebook);
                this.msg="";
                this.show=true;
            },
            del_message(index){

                this.message.splice(index,1)
                localStorage.notebook = JSON.stringify(this.message)
                this.notebook= JSON.parse(localStorage.notebook);
                if(this.message.length===0){
                    this.show=false
                }
            },
            del_all(){
                this.message=[];
                localStorage.removeItem("notebook")
                this.show=false
            }
        }
    }
</script>

<style scoped>

</style>
