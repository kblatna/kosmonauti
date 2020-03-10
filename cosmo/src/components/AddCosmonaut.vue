<template>
    <div>
        <div class="new-cosmonaut" v-for="(cosmonaut, index) in cosmonauts">

            <h2>Add new cosmonaut</h2>
            <p>Please fill in data about new cosmonaut:</p>
            <div class="new-cosmonaut--input"><label><strong>Name:</strong> </label><input v-model="cosmonaut.name"
                    type="text" placeholder="John" required></div>

            <div class="new-cosmonaut--input"><label><strong>Surname:</strong> </label><input
                    v-model="cosmonaut.surname" placeholder="Smith" required></div>

            <div class="new-cosmonaut--input"><label><strong>Birth:</strong> </label><input id="dataField"
                    v-model="cosmonaut.birth" type="text" placeholder="DD-MM-YYYY" required
                    pattern="[0-9]{4}-[0-9]{2}-[0-9]{2}" title="Enter a date in this formart DD-MM-YYYY."></div>

            <div class="new-cosmonaut--input"><label><strong>Superpower:</strong> </label><input
                    v-model="cosmonaut.superpower" placeholder="strongness" required></div>

            <div class="new-cosmonaut--button-holder">
                <button @click="deleteCosmonaut(index)">
                    <font-awesome-icon icon="trash" size="2x"></font-awesome-icon>
                </button>
                <button @click="addJson(index)">
                    <font-awesome-icon icon="plus" size="2x"></font-awesome-icon>
                </button>
            </div>
        </div>

        <button class="new-cosmonaut--add" @click="addCosmonaut">
            <font-awesome-icon icon="user-plus" size="2x"></font-awesome-icon>
        </button>
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
            this.cosmonauts.push({
                name: '',
                surname: '',
                birth: '',
                superpower: ''
            });
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
        test() {
            document.getElementById("dateField").value = new Date().toISOString().substring(0, 10)
        }
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

    .new-cosmonaut {
        width: 100%;
        max-width: 300px;
        box-shadow: 0 0 6px 0 rgba(0, 0, 0, 0.2);
        border-radius: 3px;
        margin: 30px;
        padding: 50px;
        text-align: left;
        background-color: white;
        position: absolute;
        top: 30%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .new-cosmonaut--input {
        margin: 25px 0;
    }

    .new-cosmonaut--input input {
        height: 30px;
        border: none;
        padding-left: 10px;
        box-shadow: 0 0 6px 0 rgba(0, 0, 0, 0.3);
        border-radius: 4px;
    }

    .new-cosmonaut--input label {
        padding-right: 15px;
    }

    .new-cosmonaut--button-holder {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 10px 0;
        margin-bottom: 0;
    }

    .new-cosmonaut--button-holder button {
        border: none;
        background-color: transparent;
        cursor: pointer;
    }

</style>