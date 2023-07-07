<template>
    <div class="task"
    :class="[Iscomplete ? 'Complete':'incomplete']  " >
        <div class="content" >
            <h3>{{ context }}</h3>
        </div>
        <div class="key">
            <button class='keywork up' @click='sendup' v-if='showup' >UP</button>
            <button class='keywork down' @click='senddown' v-if="showup+1!==showdown">DOWN</button>
            <button class='keywork done'  @click='setDone'>DONE</button>
        </div>
        <div class="delete">
            <button
            @click='send'
            >DELETE</button>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        context :{
            type:String,
            default:''
        },
        showup:{
            type:Number
        },
        showdown:{
            type:Number
        }
    },
    data(){
        return {
            Iscomplete:false,
            
        }
    },
    methods:{
        send(e){
            var data=new String()
            data=this.context
            this.$emit('sendata',{data})
        },
        setDone(){
            this.Iscomplete=true
        },
         sendup(e){
            var data=new String()
            data=this.context
            this.$emit('sendataup',{data})
        },
          senddown(e){
            var data=new String()
            data=this.context
            this.$emit('sendatadown',{data})
        },

    }
}
</script>


<style scoped>
    .task{
        display: flex;
        border: 1px solid black;
        border-radius: 10px;
        margin: 20px 5px 0 5px;
        background-color: #332f4c;
        color: #fff;
        min-height: 50px;
        max-width: 380px;
        transition: all 0.4s ease;
    }
    .Complete{
        background-color: #4CAF50; /* Màu nền */
        color: white; /* Màu chữ */
        border-radius: 5px; 
    }
    .incomplete{
        background-color: #ff0000;
        color:#f8d7da;
        border-radius: 4px;
            }
    .content{
        flex:3;
        word-wrap: break-word;
        padding-left: 10px;
        width: 150px;
    }
    .content>h3{
        overflow-wrap: break-word;
    }
    .key{
        flex:3; 
        box-sizing: border-box;
        display: flex;   
        align-items: center;
    }
    
    .keywork{
        max-width: 60px;
        max-height: 30px;
        padding: 10px;
        font-size: 10px;
        border-radius: 10px;
        margin-left: 5px;

    }
    .up{
       flex:1;
       background-color: #6ad37a;
    }
    .down{
       flex:2;
       background-color: #6ad37a;
    }
    .done{
        flex: 2;
        background-color: #6ad37a;
    }
    .delete{
        flex: 1;
        display: flex;
         align-items: center;
        justify-content: center;
    }
    .delete>button{
        border-radius: 10px;
        background-color: #ca3142;
        width: 45x;
        height: 30px;
        margin-left: 10px;
       
    }
</style>