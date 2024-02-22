<template>
    <div class = 'Card'>
        <div class="background">
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="702"
                height="670"
                viewBox="0 0 702 670"
                fill="none"
            >
                <path
                d="M0.206787 0H538.207L702 670H181.74L0.206787 0Z"
                fill="#FED766"
                />
            </svg>
        </div>
        <div class='left'>
            <div class ='row-50 First'>
                <div class ='ItemContainer'>
                    <Carrousel/>
                </div>
            </div>
            <div class ='row-50 Second'>
                <Prices/>
            </div>
        </div>
        <div class ='right'>
            <div class ='PaymentForm'>
                <PaymentForm/>
            </div>
        </div>
        <IconX/>
    </div>
</template>

<script>
    import IconX from './icons/IconX.vue';
    import PaymentForm from './PaymentForm.vue';
    import Carrousel from './Carrousel.vue';
    import Prices from './Prices.vue';

    import CreditCard from 'creditcard.js';
    
    export default {
    components: {
        IconX,
        PaymentForm,
        Carrousel,
        Prices,
    },
    };
</script>


<style scoped> 
    .background {
    position: absolute;
    left: 20%;
    }
    .Card {
        box-shadow: 7px 7px 12px rgba(0, 0, 0, 35%);

        color: black;

        width: 904px;
        height: 670px;
        flex-shrink: 0;
        border-radius: 20px;
        background: #e5e5e5;

        position: relative;
        display: flex;
        background: #e5e5e5 center 1px;
        margin-right: auto;
    }


    .left{
        width: 364px;
        height: 100%;
    }

    .left > .row-50{
        height: 50%;
        background-color: (81, 0, 255);
    }

    .left > .row-50.First{
        padding-left: 92px;
        padding-top: 43px;
        padding-bottom: 6px;
    }

    .left > .row-50.Second{
        background-color: hsl(0, 0%, 90%);
        margin-top: 20px;
        margin-left: 12px;
        height: 268px;
        width: 328px;
        height: 308px;
        flex-shrink: 0;
        border-radius: 10px;
    }


    .left > .row-50 > .ItemContainer{
            width: 262px;
            height: 262px;
            flex-shrink: 0;
            border-radius: 10px;
            background: #FFF;
            box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
            padding-left: 11px;
            padding-right: 10px;
            padding-top: 14px;
            display: flex;
            flex-direction: column;
    }

    .PaymentForm{
        width: 446px;
        height: 493px;
        flex-shrink: 0;
        margin-top: 93px;
    }
    .ItemContainer {
        position: relative;
    }


</style>