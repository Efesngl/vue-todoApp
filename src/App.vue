<template>
  <div class="container vh-100 w-50 mt-2">
    <h2 class="text-center">ToDo</h2>
    <hr />
    <inputText text="Todo giriniz..." :inputAction="addTodo" />
    <hr />
    <div class="container overflow-y-auto" style="height:auto;max-height:50%;">
      <ListItem :deleteTodo="deleteTodo" :text="i.text" :id="i.id" :checked="i.checked" :checkTodo="checkTodo" v-for="i in filteredTodo" />
    </div>
    <hr>
    <div class="row">
      <div class="col-12">
        <input type="checkbox" @click="showChecked=!showChecked" class="form-check-input"> Yapılanları gizle
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ListItem from "./components/ListItem.vue";
import inputText from "./components/inputText.vue";
export default {
  data() {
    return {
      showChecked:true,
      todos: [],
    };
  },
  components: {
    ListItem,
    inputText,
  },
  methods: {
    addTodo(e) {
      let item = {
        text: e.target.value,
        checked: false,
      };
      axios.post("http://localhost:3000/todos", item).then(() => {
        e.target.value = "";
        this.setTodo();
      });
    },
    setTodo() {
      axios.get("http://localhost:3000/todos").then((res) => {
        this.todos = [...res.data];
      });
    },
    deleteTodo(id) {
      axios.delete("http://localhost:3000/todos/" + id).then((res) => {
        console.log(res);
        this.setTodo();
      });
    },
    checkTodo(id,checked){
      axios.patch("http://localhost:3000/todos/"+id,{checked:!checked}).then(()=>{
        this.setTodo()
      })
    }
  },
  mounted() {
    axios.get("http://localhost:3000/todos").then((res) => {
      this.todos = [...res.data];
    });
  },
  computed:{
    filteredTodo(){
      if(!this.showChecked){
        return this.todos.filter(i=>{return i.checked==false})
      }
      return this.todos
    }
  }
};
</script>
