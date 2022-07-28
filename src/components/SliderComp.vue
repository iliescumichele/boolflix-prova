<template>
    <div class="slider">

        <div class="images">
            <img v-for="(poster, index) in posters" v-bind:key="index"
                :src="`https://image.tmdb.org/t/p/w342/${poster.poster_path}`" alt="">
        </div>
        <div class="images">
            <img v-for="(poster, index) in posters" v-bind:key="index"
                :src="`https://image.tmdb.org/t/p/w342/${poster.poster_path}`" alt="">
        </div>

    </div>
</template>

<script>
export default {
    name: 'SliderComp',
    props: {
        posters: Array
    }
}
</script>

<style lang="scss" scoped>
    .slider {

        $min-image-size: 400px;
        $max-image-size: 400px;
        $height: 600px;

        --image-size: #{$max-image-size};

        height: #{$height};
        overflow: hidden;
        width: 100%;
        margin: 0 auto;
        position: relative;
        display: flex;

        &:hover > .images{
            animation-play-state: paused;
            cursor: pointer;
            //filter: brightness(1);
        }

        // h3{
        //     position: absolute;
        //     z-index: 999;
        //     top: 100px;
        //     left: 50px;
        //     font-size: 5rem;
        // }

        .images {
            height: 100%;
            display: flex;
            position: relative;
            animation: marquee 30s linear infinite;
            justify-content: space-around;
            cursor: pointer;
            filter: brightness(.8);

            

            // Debug: This is just to help see where the loop happens
            // &:nth-of-type(1) { &, img { border:1px dashed red;  }}
            // &:nth-of-type(2) { &, img { border:1px dashed blue; }}

            // You may need this if there are too few images for the banner width
            //min-width:100%;

        }

        img {
            display: block;
            height: 100%;
            margin: 0 .5vw;
        }

        &:after {
            content: "";
            position: absolute;
            width: 100%;
            height: 100%;
            left: 0;
            top: 0;
            background: linear-gradient(to right, black, rgba(black, 0) 80px, rgba(black, 0) calc(100% - 80px), black);
        }

        @media (max-width:900px) {
            --image-size: #{$min-image-size};
            --image-size: min(max(#{$min-image-size}, 10vw), #{$max-image-size});
        }

    }

    @keyframes marquee {
        0% {
            transform: translateX(0%);
        }

        100% {
            transform: translateX(-100%);
        }
    }
</style>