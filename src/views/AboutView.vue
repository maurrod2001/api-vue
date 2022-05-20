<template>
  <div class="about">
    <h1>This is an about page</h1>
    <api msge="test"/>
  </div>
</template>
<script>
import api from '@/components/api.vue'

export default {
  name:'AboutView',
  components:{
    api
  }
}


</script>
