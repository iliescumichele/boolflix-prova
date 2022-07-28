<template>
    <div>

        <h1> {{ titleCards }}</h1>
        <div class="cards-wrapper d-flex flex-wrap justify-content-around">
            <CardComp v-for="card in items" :key="card.id" :cardData="card" />
        </div>


    </div>
</template>

<script>
import CardComp from './CardComp.vue'


export default {
    name: 'MainComp',
    components: {
        CardComp
    },
    props: {
        items: Array,
        titleCards: String,
        posters: Array
    }
}
</script>

<style lang="scss" scoped>

</style>