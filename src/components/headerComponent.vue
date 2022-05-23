<template>
    <div class="header">
        <div class="logo">
            <p>logo</p>
        </div>

        <div class="components">
            <div class="searchbar">
                <input type="text" placeholder="Search"
                    v-model.trim="textToSearch"
                    @keyup.enter="$emit('searchMovie', textToSearch)"
                >
            </div>


            <div class="select">
                <select >
                    <option disabled value selected>Seleziona cosa guardare</option>
                    <option >Movie</option>
                    <option >TV</option>
                </select> 
            </div>
        </div>


    </div>
</template>

<script>

export default {
    name: 'headerComponent',
    data(){
        return{
            textToSearch: '',
        }
    }
}
</script>

<style lang="scss" scoped>
    .header{
        padding: 20px;
        height: 80px;
        opacity: 50;
        display: flex;
        align-items: center;
        justify-content: space-between;
        background-color: rgba(0, 0, 0, 0.196);

        .components{
            display: flex;
            align-content: center;
        }
    }
</style>