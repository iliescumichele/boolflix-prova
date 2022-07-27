<template>
  <header>
    <header>
        <input @keyup.enter="startSearch" v-model.trim="titleToSearch" type="text" placeholder="Search content">
    </header>
  </header>
</template>

<script>
export default {
    name: 'HeaderComp',
    data() {
        return {
            titleToSearch: ''
        }
    },

    methods: {
        startSearch(){
            this.$emit( 'startSearch', this.titleToSearch );
            this.titleToSearch = '';
        }
    },
}

</script>

<style lang="scss" scoped>

</style>