<template>
  <div class="row justify-content-center mb-2" v-for="(item,index) in filteredTodo" :key="item.id">
    <div class="col-6 d-flex justify-content-between">
      <div class="col-1 d-inline-block">
        <input class="form-check-input" type="checkbox" :checked="item.checked" name="" id="" @click="checkTodo(item.index,$event)" />
      </div>
      <div class="col-9 d-inline-block ms-1" :class="{ 'text-decoration-line-through': item.checked }">{{ item.text }}</div>
      <div class="col-2 text-center d-inline-block">
        <button class="btn btn-danger" @click="removeTodoItem(item.index)">sil</button>
      </div>
    </div>
    </div>
  <div class="row justify-content-center">
    <div class="col-6">
      <hr />
      <input type="checkbox" name="" id="" @click="showChecked = !showChecked" :checked="showChecked" />
      Yapılanları göster
    </div>
  </div>
</template>

<script>
export default {
  inject:["todos"],
  data(){
    return {
      showChecked:true
    }
  },
  methods:{
    checkTodo(i,e){
      this.todos.forEach((item)=>{
        if(item.index==i){
          item.checked=e.target.checked
        }
      })
    },
    removeTodoItem(pIndex){
      let todoIndex=this.todos.findIndex((item)=>{return item.index==pIndex})
      this.todos.splice(todoIndex,1)
    }
  },
  computed: {
    filteredTodo() {
      if(this.showChecked==false){
        return this.todos.filter(todo=>{return !todo.checked})
      }
      return this.todos
    },
  },
};
</script>
