<template>
    <div class="home">

        <h1>Cosmonaut's list</h1>
        <p>There are our great cosmonauts. You can see, what superpower they have.
            You can also delete any of them or add a new one. Editing of existing
            cosmonaut is not possible yet, but we work on it! If you have any comments
            or tips for improvements, please <a href="mailto:katerina.blatna@email.cz">
            contact me</a> :)</p>

        <cosmonaut :onAdd="newCosmonaut" />
        <addcosmonaut @newCosmonaut="addNewCosmonaut" />
    </div>
</template>

<script>

import Cosmonaut from '@/components/Cosmonaut.vue'
import AddCosmonaut from '@/components/AddCosmonaut.vue'

export default {
    name: 'home',

    data() {
        return {
            newCosmonaut: null
        }
    },

    components: {
        'cosmonaut': Cosmonaut,
        'addcosmonaut': AddCosmonaut
    },

    methods: {
        addNewCosmonaut(data) {
            this.newCosmonaut = data;
        }
    }
}
</script>

<style scoped>

p {
    margin: 0 25%;
}

a {
    color: #2c3e50;
    text-decoration: none;
    font-weight: 700;
}

a:hover {
    color: #575756;
}

</style>


