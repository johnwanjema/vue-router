<template>
    <div>
        <p>Name: {{ coin.name }}</p>
        <p>Symbol: {{ coin.symbol }}</p>
        <p>Price (USD): {{ coin.price_usd }}</p>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Coins',

    data() {
        return {
            coin: {}
        }
    },

    created() {
        this.fetchData()
    },
// watch used to check for changes in the request and reload the data
    watch: {
        '$route': 'fetchData'
    },

    methods: {
        // use axios to fetch the data
        fetchData() {
            axios.get('https://api.coinmarketcap.com/v1/ticker/' + this.$route.params.id + '/')
                .then((resp) => {
                    this.coin = resp.data[0]
                    console.log(resp)
                })
                .catch((err) => {
                    console.log(err)
                })
        }
    }
}
</script>