<template>
    <div class="card-container">


        <div class="card-movie"
            v-for="(item, index) in trends"
            :key="index"
        >
            <h3>{{item.title}}</h3>
            <h4>{{item.original_title}}</h4>
            <p>{{item.original_language}}</p>
            <span>{{item.vote_count}}</span>
        </div>
    </div>
</template>

<script>

export default {
    name: 'mainComponent',
    props: {
        movie: Array,
        trends: Array,
        tvSeries: Array,
        txtFromSelect: String
    }
}
</script>

<style lang="scss" scoped>
    .card-container{
        width: 80%;
        margin: 0 auto;
        border: 1px solid white;
        color: white;
        display: flex;
        flex-wrap: wrap;

        .card-movie{
            margin: 15px;
            border: 1px solid red;
            width: calc(100% / 5)
        }
    }
</style>