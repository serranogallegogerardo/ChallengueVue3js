<template>
    <div>
        <h1 class = 'Title'>Sneekers for Men</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt</p>

        <!-- aca podria colocar unos ifs -->
        <h4 class = 'titleBTC'>Price in BTC</h4>
        <div class = 'showBTC'>₿ {{ priceShoesBTC }}</div>
        <h4 class = 'titleUSD'>Price in USD</h4>
        <div class = 'showUSD'>${{ priceShoes.toFixed(2) }}</div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const priceBTC = ref(0);
const priceShoes = ref(69.00); // Precio de los zapatos en moneda local
const priceShoesBTC = ref(0);

const fetchBitcoinPrice = async () => {
    try {
            const response = await fetch("https://api.blockchain.com/v3/exchange/tickers");
            const data = await response.json();
            const bitcoinPrice = data.find(item => item.symbol === 'BTC-USD').last_trade_price;
            
            // priceBTC.value = bitcoinPrice;
            priceShoesBTC.value = (priceShoes.value / bitcoinPrice).toFixed(10);
    } catch (error) {
            console.error('Error fetching Bitcoin price:', error);
    }
};

// Llama a fetchBitcoinPrice al montar el componente
onMounted(() => {
    fetchBitcoinPrice();
    // Actualiza el precio cada 5 segundos
    setInterval(fetchBitcoinPrice, 5000);
});
</script>

<style scoped>

    
    div h1.Title{
        width: 290px;
        height: 43px;
        flex-shrink: 0;

        color: #363537;

        font-family: Roboto;
        font-size: 36px;
        font-style: normal;
        font-weight: 700;
        line-height: normal;

        margin-left: 14px;
        margin-right: 24px;

    }

    div p{
        width: 290px;
        height: 30px;
        flex-shrink: 0;

        color: #363537;
        text-align: center;
        font-family: Roboto;
        font-size: 14px;
        font-style: normal;
        font-weight: 300;
        line-height: normal;

        margin-left: 13px;
        margin-right: 25px;

    }

    div h4.titleBTC {

        margin-top: 31px;
        margin-left: 14px;
        margin-right: 114px;

        width: 200px;
        height: 35px;
        flex-shrink: 0;


        color: #363537;

        font-family: Poppins;
        font-size: 20px;
        font-style: normal;
        font-weight: 500;
        line-height: normal;

        color: #363537;

    }

    div h4.titleUSD {
        margin-top: 13px;
        margin-left: 14px;
        margin-right: 114px;

        width: 200px;
        height: 35px;
        flex-shrink: 0;


        color: #363537;

        font-family: Poppins;
        font-size: 20px;
        font-style: normal;
        font-weight: 500;
        line-height: normal;
    }

    div div.showBTC{
        width: 169px;
        height: 29px;
        flex-shrink: 0;
        color: #363537;
        font-family: Poppins;
        font-size: 20px;
        font-style: normal;
        font-weight: 700;
        line-height: normal;

        margin-left: 14px;
    }

    div div.showUSD{
        color: #363537;
        font-family: Poppins;
        font-size: 20px;
        font-style: normal;
        font-weight: 700;
        line-height: normal;
        margin-left: 14px;
    }

    div > * {
        position: relative;
    }

</style>