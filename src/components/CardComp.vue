<template>
    <div class="card">
        <h3>{{cardData.original_title }}</h3>
        <h3>{{ cardData.title }}</h3>
        <p>{{ cardData.original_language }}</p>
        <p>{{ cardData.vote_average }}</p>
        <hr>
    </div>
</template>

<script>
export default {
    name: 'CardComp',
    props: {
        cardData: Object
    }
}
</script>

<style lang="scss" scoped>

</style>