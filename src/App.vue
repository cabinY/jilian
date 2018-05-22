<template>
  <div>
    <city></city>
    <lian2></lian2>
  </div>
</template>

<script>
import Lian from './component/lian.vue'
import City from './component/city.vue'
export default {
  name: 'app',
  components:{
    Lian,City
  },
  data () {
    return {
      per:50
    }
  },
}
</script>

