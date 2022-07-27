<template>
  <header>
    <header>
        <input @keyup.enter=" $emit( 'startSearch', titleToSearch )" v-model.trim="titleToSearch" type="text">
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
}

</script>

<style lang="scss" scoped>

</style>