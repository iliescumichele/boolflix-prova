<template>
    <main>
        <h1> {{ titleCards }}</h1>

        <CardComp 
            v-for="card in items"
            :key="card.id"
            :cardData="card"
        />
    
    </main>
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
        titleCards: String
    }
}
</script>

<style lang="scss" scoped>

</style>