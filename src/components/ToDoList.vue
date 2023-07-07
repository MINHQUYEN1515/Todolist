<template>
  <div id="app">
    <div class="header">
      <h1>TASK BOARD</h1>
      <p>Create a list of task</p>
    </div>
    <main>
      <div class='inputlist'>
        <input type="text" placeholder="Add a new list" v-model="text" @keyup.enter='Addnewtask'>
        <button @click='Addnewtask'>ADD</button>
        <div class='boder'></div>
      </div>
      <ListTask v-bind:Value='task'
      v-bind:maxlength='maxlength'
      @sendata='getdatavalue'
      @sendata_up='changeindexup'
       @sendata_down='changeindexdown'
      />
    </main>
  </div>
</template>

<script>
import ListTask from './List.vue'
export default {
    data(){
      return{
        text:'',
        task:[],
        maxlength:0
      }
    },
    components:{
      ListTask
    },
    methods:{
      Newtask(){
        console.log(text)
      },
      Addnewtask(){
        if(!this.text){
          alert("Vui lòng nhập công việc")
        }
        else{
        this.task.push(
          {
            context:this.text,
          }
        )
        this.maxlength=this.task.length
        this.text=''
        }
      },
      getdatavalue(data){
        var indexdelete=-1
        this.task.forEach((Task,index)=>{
          if(Task.context===data.data){
            indexdelete=index
          }
          
        })
        this.task.splice(indexdelete,1)
      },
      changeindexup(data){
          var indexchange=-1
        this.task.forEach((Task,index)=>{
          if(Task.context===data.data){
            indexchange=index
          }
          
        })
        swap(this.task,indexchange,indexchange-1)
        
      },
       changeindexdown(data){
          var indexchange=-1
        this.task.forEach((Task,index)=>{ 
            if(Task.context===data.data){
              indexchange=index
            }
        })

        swap(this.task,indexchange,indexchange+1)
      
        
      }
      
    },
    computed:{
      setmaxlength(){
        return this.maxlength=this.task.length
      }
    }
    
}

    function swap(arr, index1, index2) {
        var temp = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = temp;

      }
      
</script>
<style scoped>
  #app{
    border: 1px solid black;
    width: 400px;
    min-height: 600px;
    margin-left: 500px;
    background-color: #377e7f;
  }
  .header{
    text-align: center;
    color: #fff;
  }

  .inputlist>input{
    width: 250px;
    height: 30px;
    margin-left: 30px;
    border: none;
    background-color: transparent;
    font-size: 16px;
    outline: none;
    color: #fff;
   
  }
  .inputlist>button{
    width: 80px;
    height: 50px;
    border-radius: 5px;
    background-color: #6ad37a;
    color:black;
    font-weight: 1000;
  }
  .boder{
    width: 250px;
    height: 1px;
    background-color: #fff;
    margin-left: 30px;
    margin-top: -10px;
  
  }
  input::placeholder{
    color: #fff;
  }
</style>