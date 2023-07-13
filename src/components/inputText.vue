<template>
    <div class="row">
        <div class="col-12">
          <input type="text" @keypress.enter="inputAction" :placeholder="text" class="form-control">
        </div>
      </div>
</template>

<script>
    export default{
        props:["text","inputAction"]
    }
</script>