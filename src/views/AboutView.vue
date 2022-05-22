<template>
  <div class="about">
    <h1>This is an about page</h1>
    <api msg="test"/>
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
