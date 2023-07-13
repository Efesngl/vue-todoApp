<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-6 text-center">
        <h3>ToDo</h3>
        <hr />
      </div>
    </div>
    <AddTodo></AddTodo>
    <TodoList></TodoList>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';
import AddTodo from './components/AddTodo.vue';
import { computed } from 'vue';
export default {
  provide(){
    return {
      todos:computed(()=>this.todos),
      addTodo:this.addTodo,
      todoEmpty:computed(()=>this.isEmpty)
    }
  },
  data() {
    return {
      isEmpty:false,
      index: null,
      todos: [
        { text: "Vue öğren", checked: false, index: 1 },
        { text: "PHP öğren", checked: true, index: 2 },
        { text: "Web dev olarak iş bul", checked: false, index: 3 },
      ],
    };
  },
  methods: {
    addTodo(data) {
      if(data.replace(/\s/g,"").length){
        let index = this.index;
      let item = {
        text: data,
        checked: false,
        index: ++index,
      };
      this.index++;
      this.todos.push(item);
        if(this.isEmpty==true) this.isEmpty=false
      }
      else{
        this.isEmpty=true
      }
    },
  },
  mounted() {
    this.index = this.todos.length;
  },
  components:{
    TodoList,
    AddTodo
  }
};
</script>
