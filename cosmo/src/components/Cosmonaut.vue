<template>
  <div class="cosmonaut">
      <div class="cosmonaut--box" v-for="(item, index) in items">

        <img :src="require('../assets/images' + item.image)" :alt="item.alt"/>

        <div class="cosmonaut--box__inner">

            <h3>{{item.name}} {{item.surname}}</h3>
            <p><strong>Birth:</strong> {{item.birth}}</p>
            <p><strong>Superpower:</strong> {{item.superpower}}</p>

            <div class="cosmonaut--box__button-holder">

              <button @click="deleteEvent(index)"><font-awesome-icon icon="trash" size="2x"></font-awesome-icon></button>
              <button><font-awesome-icon icon="edit" size="2x"></font-awesome-icon></button>

            </div>
        </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
import AddCosmonaut from '@/components/AddCosmonaut.vue'

export default {
  name: 'cosmonaut',
	data() {
		return {
      items: []
		}
	},
	mounted() {
		this.fetchItems()
  },
	methods: {
    fetchItems() {
			  let id = this.$route.params.id;
        let url = '/cosmonauts.json';

        axios.get(url)
             .then(response => {
        this.items = response.data
      });
    },
    deleteEvent: function(index) {
      this.items.splice(index, 1);
    }
  },

	watch: {
    '$route.params.id': 'fetchItems'
  }
}

</script>

<style scoped>

.cosmonaut {
    display: flex;
    flex-wrap: wrap;
}

.cosmonaut--box {
    width: 100%;
    max-width: 300px;
    box-shadow: 0 0 6px 0 rgba(0,0,0,0.2);
    border-radius: 3px;
    margin: 30px;
}

.cosmonaut--box__inner {
    margin: 20px;
}

h3 {
    font-weight: 700;
}

.cosmonaut--box img {
    width: 100%;
    height: 200px;
    object-fit: contain;
    border-top-left-radius: 3px;
    border-top-right-radius: 3px;
}

.cosmonaut--box__button-holder {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 0;
}

.cosmonaut--box__button-holder button {
    border: none;
    background-color: transparent;
    cursor: pointer;
}



</style>
