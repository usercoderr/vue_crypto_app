<template>
    <input min="0" @input="changeAmount($event.target.value)" type="number"/>
    <br/>
    <button @click="convert()">Convert</button>
    <div>
    <button @click="favorite()">To Favorites</button>
    </div>
</template>
<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        },
        convert: {
            type: Function,
            required: true
        },
        favorite: {
            type: Function,
            required: true
        }
    }
}
</script>


<style scoped>
input {
    outline: none;
    width: 500px;
    border-radius: 3px;
    border: 0;
    padding: 10px 15px;
}
button{
    border: 0;
    border-radius: 6px;
    background: #1A032D;
    color: wheat;
    padding: 14px 18px;
    cursor: pointer;
    margin-top: 20px;
}
button:hover {
    background: #7613c7;
    cursor: pointer;
}
</style>
