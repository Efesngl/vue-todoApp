<template>
    <div class="row mb-2">
        <div class="col-1">
          <input type="checkbox" :checked="checked" @click="checkTodo(id,checked)"  class="form-check-input" name="" id="" />
        </div>
        <div class="col-9" :class="{'checked':checked}">{{ text }}({{ id }})</div>
        <div class="col-2">
          <button class="btn btn-danger" @click="deleteTodo(id)">Sil</button>
        </div>
      </div>
</template>
<script>
    export default{
        props:["deleteTodo","text","id","checked","checkTodo"]
    }
</script>

<style>
    .checked{
        text-decoration: line-through;
    }
</style>