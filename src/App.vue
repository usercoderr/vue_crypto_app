<template>
    <h1>CRYPTO</h1>
    <Input :favorite="favorite " :change-amount="changeAmount" :convert="convert"/>
    <p v-if="error !== ''">{{ error }}</p>
    <div class="selectors">
        <Selector :crypto-now="cryptoFirst" :set-crypto="setCryptoFirst"/>
        <Selector :crypto-now="cryptoSecond" :set-crypto="setCryptoSecond"/>
    </div>
    <p v-if="result !== 0" class="result">{{ result }}</p>
    <Favorite
            :get-from-favorites="getFromFavorites"
            :favorites="favorites" v-if="favorites.length > 0"/>
</template>


<script>
import {defineComponent} from "vue";
import Input from "./components/ui/Input.vue";
import Selector from "./components/ui/Selector.vue";
import CryptoConvert from "crypto-convert";
import Favorite from "./components/Favorite.vue";

const convert = new CryptoConvert()
export default defineComponent({
    components: {Favorite, Selector, Input},
    data() {
        return {
            amount: 0,
            cryptoFirst: '',
            error: '',
            cryptoSecond: '',
            result: 0,
            favorites: []
        }
    },
    methods: {
        getFromFavorites(index) {
            this.cryptoFirst = this.favorites[index].from
            this.cryptoSecond = this.favorites[index].to
        },
        favorite() {
            this.favorites.push({
                from: this.cryptoFirst,
                to: this.cryptoSecond
            })
        },
        changeAmount(val) {
            this.amount = val
        },
        setCryptoFirst(val) {
            this.cryptoFirst = val
        },
        setCryptoSecond(val) {
            this.cryptoSecond = val
        },
        async convert() {
            if (this.amount <= 0) {
                this.error = 'Enter number more than 0'
            } else if (this.cryptoFirst === this.cryptoSecond) {
                this.error = 'Choose another value'
            } else if (this.cryptoFirst === '' || this.cryptoSecond === '') {
                this.error = 'Choose  value'
            }
            this.error = ''


            await convert.ready()
            if (this.cryptoFirst === 'BTC' && this.cryptoSecond === 'ETH') {
                this.result = convert.BTC.ETH(this.amount)
            } else if (this.cryptoFirst === 'BTC' && this.cryptoSecond === 'USDT') {
                this.result = convert.BTC.USDT(this.amount)
            } else if (this.cryptoFirst === 'ETH' && this.cryptoSecond === 'BTC') {
                this.result = convert.ETH.BTC(this.amount)
            } else if (this.cryptoFirst === 'ETH' && this.cryptoSecond === 'USDT') {
                this.result = convert.ETH.USDT(this.amount)
            } else if (this.cryptoFirst === 'USDT' && this.cryptoSecond === 'BTC') {
                this.result = convert.USDT.BTC(this.amount)
            } else if (this.cryptoFirst === 'USDT' && this.cryptoSecond === 'ETH') {
                this.result = convert.USDT.ETH(this.amount)
            }
        }
    }
})
</script>

<style scoped>
.selectors {
    display: flex;
    justify-content: space-around;
    width: 800px;
    margin: 20px auto;
}

.result {
    font-family: 'Cinzel', cursive;
    color: yellow;
    margin-top: 10px;
    font-size: 2em;
}
</style>
