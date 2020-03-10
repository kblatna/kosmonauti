<template>
    <div class="home">
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


