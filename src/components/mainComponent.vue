<template>
    <div class="card-container">


        <div class="card"
            v-for="(item, index) in trends"
            :key="index"
        >
            <h3>{{item.title || item.name}}</h3>
            <h4>{{item.original_title || item.original_name}}</h4>
            <div class="flag-language">
                <img v-if="item.original_language === 'it'"    
                    src="../assets/img/flag-ita.png" alt="item.original_language"
                >
                <img v-else-if="item.original_language === 'en'"    
                    src="../assets/img/flag-uk.png" alt="item.original_language"
                >
                <p v-else>{{item.original_language}}</p>
            </div>
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

        .card{
            margin: 15px;
            border: 1px solid red;
            width: calc(100% / 5);

            .flag-language{
                width: 70px;

                img{
                    width: 100%;
                }
            }
        }
    }
</style>