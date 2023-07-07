<template>
    <div>
        <Task
        v-for='(task,index) in Value'
        v-bind:key=index
        v-bind:showdown='maxlength'
        v-bind:showup='index'
        v-bind:context='task.context'
        @sendata='getdata'
        @sendataup='getdataup'
        @sendatadown='getdatadown'
        
        ></Task>
    </div>
</template>

<script>
import Task from'./Task.vue'
export default {
    props:{
        Value:{
            type:Array,
            default:[]
        },
        maxlength:{
            type:Number
        }
    },
    data(){
        return{}
    },
    components:{
        Task
    },
    methods:{
    getdata(data){
        this.$emit('sendata',data)
    },
      getdataup(data){
        this.$emit('sendata_up',data)

    },
      getdatadown(data){
        this.$emit('sendata_down',data)

    }
    }
}
</script>


<style scoped>

</style>