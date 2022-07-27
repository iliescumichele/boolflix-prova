<template>
  
    <header class="d-flex justify-content-between align-items-center px-3">

        <div class="logo">
            <img src="../assets/img/logo-netflix.png" alt="Logo Boolflix">
        </div>

        <div class="inputs d-flex">
            <input class="form-control mx-4" @keyup.enter="startSearch" v-model.trim="titleToSearch" type="text" placeholder="Search content">

            <select class="form-control" v-model="typeToSearch" @change="startSerch">
                <option selected disabled value="">Seleziona film / serieTV</option>
                <option value="all">All</option>
                <option value="movie">Movies</option>
                <option value="tv">TV Series</option>
            </select>
        </div>

    </header>
  
</template>

<script>
export default {
    name: 'HeaderComp',
    data() {
        return {
            titleToSearch: '',
            typeToSearch: 'all'
        }
    },

    methods: {
        startSearch(){
            this.$emit( 'startSearch', this.titleToSearch, this.typeToSearch );
            this.titleToSearch = '';
        }
    },
}

</script>

<style lang="scss" scoped>
    @import '../assets/style/vars';

    header{
        position: fixed;
        z-index: 999;
        top: 0;
        width: 100%;
        height: 75px;
        background-image: linear-gradient(black, $bg-color);

        .logo{
            height: 100%;
            padding-top: 10px;
            img{
                height: 80%;
            }
        }

        input{
            min-width: 400px;
        }
        select{
            width: 150px;
            text-align: center;
        }
    }
</style>