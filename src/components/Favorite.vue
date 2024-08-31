<template>
    <h2>Favorites:</h2>
    <br/>
    <div @click="getFromFavorites(index)" v-for="(el, index) in favorites" :key="index">
        <p>{{ index + 1 }}. <span>{{ el.from }}-</span> <span> {{ el.to }}</span></p>
    </div>
</template>
<script>
export default {
    props: {
        favorites: {
            type: Array,
            required: true
        },
        getFromFavorites: {
            type: Function,
            required: true
        }
    }
}
</script>
<style scoped>
div {
    cursor: pointer;
    color: yellow;
}

h2 {
    color: wheat;
}
p{
    margin: 8px 0;
}
</style>
