<template>
    <div class="card">
        <h3>{{cardData.original_title || cardData.original_name}}</h3>
        <h3>{{ cardData.title || cardData.name}}</h3>

        <img 
            v-if=" flags.includes(cardData.original_language)" 
            :src=" require(`../assets/img/${ cardData.original_language }.png`)" alt=""
        >

        <p v-else>Ligua: {{ cardData.original_language }}</p>
        <p>{{ cardData.vote_average }}</p>
        <hr>
    </div>
</template>

<script>
export default {
    name: 'CardComp',
    props: {
        cardData: Object
    },
    data() {
        return {
            flags: ['it', 'en']
        }
    },
}
</script>

<style lang="scss" scoped>
    img{
        width: 30px;
    }
</style>