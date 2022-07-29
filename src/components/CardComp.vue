<template>


    <div class="my-card d-flex justify-content-center">
        <flip-flop-card :elevation="7" direction="horizontal" width="300" speed="4">
            <template slot="front">
                <div class="basic-card">
                    
                    <img v-if="cardData.poster_path"
                        class="img-fluid"
                        :src="`https://image.tmdb.org/t/p/w342/${cardData.poster_path}`" 
                        alt="cardData.title || cardData.name"
                    >
                    <div v-else 
                        class="placeholder-poster d-flex justify-content-center align-items-center text-center p-3" >
                        <h3>{{ cardData.title || cardData.name }}</h3>
                    </div>
                </div>
            </template>
            <template slot="back">
                <div class=" basic-card inner p-2">
                    <div class="top">
                        <h3>{{ cardData.title || cardData.name }}</h3>
                    </div>

                    <img class="flag" v-if="flags.includes(cardData.original_language)"
                        :src="require(`../assets/img/${cardData.original_language}.png`)" alt="">
                    <p v-else>Ligua: {{ cardData.original_language }}</p>
                    <p>{{ cardData.vote_average }}</p>


                    <!-- STELLINE -->
                    <div class="">
                        <i class="fa-star fa-solid"
                            v-for="i in Math.floor( Math.round(cardData.vote_average)/2 )"
                            :key="`a${i}`">
                        </i>

                        <!-- stampo la mezza stella -->
                        <i v-if="Math.round(cardData.vote_average) % 2" class="fa-solid fa-star-half-stroke"></i> 
                        
                        <!-- stampo le stelline vuote
                            // la differenza di 5 meno stelle piene - modulo 2 del voto reale arrotondato
                        -->
                        <i class="fa-star fa-regular"
                            v-for="i in ( 5 - Math.floor( Math.round(cardData.vote_average)/2 ) - (Math.round(cardData.vote_average) % 2) )"
                            :key="`b${i}`">
                        </i>

                    </div>
                    <!-- /STELLINE -->
                    
                    <div class="overview">
                        {{cardData.overview}}
                    </div>
                
                </div>
            </template>
        </flip-flop-card>
    </div>
    

</template>

<script>
import FlipFlopCard from "vue-flip-flop-card";

export default {
    name: 'CardComp',
    components: { FlipFlopCard },
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
.my-card{
    flex-basis: 25%;
    margin-bottom: 40px;

    .basic-card{
        height: 100%;
        .placeholder-poster{
            height: 100%;
            h3{
                font-size: 3rem;
            }
        }
    }

    .inner{
        height: 100%;
        background-color: black;

        .top{
            min-height: 20%;
        }
    
        .flag {
            width: 30px;
        }

        .overview{
            height: 50%;
            overflow-y: auto;
        }
    }
}


</style>