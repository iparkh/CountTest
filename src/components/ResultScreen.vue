<template>
  <div class="alert alert-primary">
    <h3> Успішних: {{stats.success}} 
    </h3>
    <h3> Помилок: {{stats.error}} 
    </h3>
    <hr>
   <!-- <ul >
   <li v-for="res in results" >
    {{ res.x }} + {{res.y}} = {{res.z}}   
   </li>
  </ul> -->

    <button class="btn btn-primary" 
            @click="$emit('repeate')">Повторити
    </button>
    <button class="btn btn-primary"  
            @click="$emit('nextLevel')">Наступний рівень
    </button>
  </div>
</template>

<script>
  export default{
    props:['stats','results']
  }
</script>

<style>

</style>