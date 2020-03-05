<template>
  <div class="cosmonaut">

    <div id="app">
      <h1>Finds</h1>
      <div v-for="(item, index) in items">
        <label>Name: </label><input v-model="item.name">
        <label>Surname: </label><input v-model="item.surname">
        <label>Birth: </label><input v-model="item.birth">
        <label>Superpower: </label><input v-model="item.superpower">
      </div>
      <button @click="addFind">
        Add new cosmonaut
      </button>
      <!--<pre>{{ $data }}</pre>-->
    </div>

  </div>
</template>

<script>
import axios from 'axios';
import Cosmonaut from '@/components/Cosmonaut.vue'

export default {
  name: 'addcosmonaut',
  data() {
    return {
    items: []
    }
  },

  methods: {
    addFind: function () {
      this.items.push({ name: '' , surname: '', birth: '', superpower: ''});
    }
  }
}

</script>

<style scoped>



</style>
