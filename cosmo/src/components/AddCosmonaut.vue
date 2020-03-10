<template>
<div>
    <button class="new-cosmonaut--add" @click="addCosmonaut"><font-awesome-icon icon="user-plus" size="2x"></font-awesome-icon></button>

    <div class="new-cosmonaut">

        <div class="new-cosmonaut--box" v-for="(cosmonaut, index) in cosmonauts">

            <h2>Add new cosmonaut</h2>
            <div><label>Name: </label><input v-model="cosmonaut.name"></div>
            <div><label>Surname: </label><input v-model="cosmonaut.surname"></div>
            <div><label>Birth: </label><input v-model="cosmonaut.birth"></div>
            <div><label>Superpower: </label><input v-model="cosmonaut.superpower"></div>

            <div class="new-cosmonaut--box__button-holder">
                <button @click="deleteCosmonaut(index)"><font-awesome-icon icon="trash" size="2x"></font-awesome-icon></button>
                <button @click="addJson(index)"><font-awesome-icon icon="plus" size="2x"></font-awesome-icon></button>
            </div>

        </div>
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
            cosmonauts: []
        }
    },

    methods: {
        addCosmonaut: function () {
            this.cosmonauts.push({ name: '', surname: '', birth: '', superpower: '' });
        },
        addJson(index) {
            let cosmonaut = this.cosmonauts[index]
            this.$emit('newCosmonaut', {
                image: "/placeholder.jpg",
                alt: cosmonaut.name + " " + cosmonaut.surname,
                name: cosmonaut.name,
                surname: cosmonaut.surname,
                birth: cosmonaut.birth,
                superpower: cosmonaut.superpower
            })
            this.cosmonauts.splice(index, 1)
        },
        deleteCosmonaut(index) {
            this.cosmonauts.splice(index, 1);
        },
        fetchItems() {
            let id = this.$route.params.id;
            let url = '/cosmonauts.json';

            axios.get(url)
                .then(response => {
                    this.items = response.data
                });
        },
        deleteEvent(index) {
            this.items.splice(index, 1);
        },
        mounted() {
            this.fetchItems()
        },
    },
    watch: {
    '$route.params.id': 'fetchItems'
    }
}

</script>

<style scoped>

.new-cosmonaut--add {
  border: none;
  background-color: transparent;
  cursor: pointer;
  position: absolute;
  top: 20px;
  right: 20px;
}

.new-cosmonaut--box {
    width: 100%;
    max-width: 300px;
    box-shadow: 0 0 6px 0 rgba(0,0,0,0.2);
    border-radius: 3px;
    margin: 30px;
    padding:20px;
    text-align: left;
}

.new-cosmonaut--box{
  margin: 15px;
}

.new-cosmonaut--box__button-holder {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 0;
    margin-bottom: 0;
}

.new-cosmonaut--box__button-holder button {
    border: none;
    background-color: transparent;
    cursor: pointer;
}

</style>
