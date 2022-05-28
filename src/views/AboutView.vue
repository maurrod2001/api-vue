<template>
  <div class="about">
    <api msg="pacients"/>
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
