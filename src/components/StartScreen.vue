<template>
 <div class="alert alert-secondary">

   <h3>Ви готові?</h3>
   <button class="btn btn-success" @click="$emit('onStart')">Починайте</button>
 </div>
</template>

<script>
  export default {
      methods:{
        some() {
          alert(1234);
        }
      }
  }
</script>

<style scoped>
  .alert{
    text-align: center;
  }
  h3,bnt {
    margin:30px 0;
  }
</style>