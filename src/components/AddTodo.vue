<template>
    <div class="row justify-content-center mb-3">
        <div class="col-6 d-flex justify-content-between">
          <div class="col-9 d-inline-block">
            <input type="text" name="todo" id="todo" placeholder="todo ekle" class="form-control" :class="{'border-danger':todoEmpty}" @keyup.enter="afterAddTodo" v-model="todoText"/>
          </div>
          <div class="col-2 d-inline-block text-center">
            <button class="btn btn-success" @click="afterAddTodo">Ekle</button>
          </div>
        </div>
      </div>
      
</template>
<style>
  .form-control:focus{
    box-shadow: none !important;
  }
</style>
<script>
    export default{
      inject:["addTodo","todoEmpty"],
      data(){
        return {
          todoText:""
        }
      },
      methods:{
        afterAddTodo(){
          this.addTodo(this.todoText)
          this.todoText=""
        }
      }
    }
</script>