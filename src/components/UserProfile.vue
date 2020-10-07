<template>
    <div class="container-fluid ml-2">
     <div class="row">
      <div v-if="user.username" class="profile">
      <p style="color: #45b6fe">Hello {{user.username}}</p> 
      </div>
     </div>
     </div>
   
</template>

<script>
export default {
    props: ['user']
    
}
</script>
<style>

</style>