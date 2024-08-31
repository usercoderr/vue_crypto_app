<template>
    <ul>
        <li @click="setCrypto('BTC')" :class="cryptoNow === 'BTC' ? 'active' : ''">BTC</li>
        <li @click="setCrypto('ETH')" :class="cryptoNow === 'ETH' ? 'active' : ''">ETH</li>
        <li @click="setCrypto('USDT')" :class="cryptoNow === 'USDT' ? 'active' : ''">USDT</li>
    </ul>
</template>
<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true
        },
        cryptoNow: {
            type: String,
            required: true
        }
    },
}
</script>
<style scoped>
ul {

    list-style: none;
    width: 200px;
    padding: 0;
    border-radius: 3px;
    border: 3px solid #000;
}

li {
    text-align: center;
    display: block;
    color: wheat;
    background: #1A032D;
    padding: 20px 0;
}

li:hover, li.active {
    background: #7613c7;
    cursor: pointer;
}
</style>
