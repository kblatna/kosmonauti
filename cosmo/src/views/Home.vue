<template>
  <div class="home">
    <cosmonaut />
    <addcosmonaut />
  </div>
</template>

<script>

import Cosmonaut from '@/components/Cosmonaut.vue'
import AddCosmonaut from '@/components/AddCosmonaut.vue'

export default {
  name: 'home',

  components: {
    'cosmonaut': Cosmonaut,
    'addcosmonaut': AddCosmonaut
  }
}
</script>


