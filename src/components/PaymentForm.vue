<template>
    <div v-if="showForm">
        <form @submit.prevent="processPayment">
        <div class ='Container First'> 

            <label for="creditCard">Card Number</label>
            <!-- Renderizar segun el tipo de tarjeta -->
            <div v-if="creditCardName == null" class = 'logoCard'>
                <img src="https://raw.githubusercontent.com/aaronfagan/svg-credit-card-payment-icons/main/flat/generic.svg" alt = 'generic'>
            </div>
            <div v-if="creditCardName == 'Visa' " class = 'logoCard'>
                <img src="https://github.com/aaronfagan/svg-credit-card-payment-icons/raw/main/flat/visa.svg" alt = 'Visa'>
            </div>
            <div v-if="creditCardName == 'Amex' " class = 'logoCard'>
                <img src="https://github.com/aaronfagan/svg-credit-card-payment-icons/raw/main/flat/amex.svg" alt = 'Amex'>
            </div>
            <div v-if="creditCardName == 'Mastercard' " class = 'logoCard'>
                <img src="https://raw.githubusercontent.com/aaronfagan/svg-credit-card-payment-icons/0e2affe1f8fed4a29e7583df266f09272b44323d/flat/mastercard.svg" alt = 'Mastercard'>
            </div>
            <div v-if="creditCardName == 'Diners' " class = 'logoCard'>
                <img src="https://raw.githubusercontent.com/aaronfagan/svg-credit-card-payment-icons/main/flat/diners.svg" alt = 'Diners'>
            </div>
            
            <input
            class = 'IcoCC'
    
            v-model="creditCardNumber"
            maxlength="19"
            placeholder="0000 0000 0000 0000"
            @input="checkCreditCardValidity"
            onkeypress="return (event.charCode >= 48 && event.charCode <= 57)"
            />
    
            <div v-if="isCreditCardValid !== null">
            {{ isCreditCardValid ? 'The card is correct' : 'The card is invalid' }}
            </div>
        </div>
    
        <div class ='Container Second'>
            <label for="expiry">MM/YY</label>
            <input v-model="expiry" placeholder="MM/YY" maxlength="5" @input="validateExpirationDate" />
            <div v-if="isExpirationValid !== null">
            {{ isExpirationValid ? 'Valid expiration date' : 'Invalid expiration date' }}
            </div>          
        </div>
    
        <div class ='Container Third'>
            <label for="cvc">CVC Code</label>
            <input v-model="cvc" placeholder="539" maxlength="4" @input="validateCvc" />
            <div v-if="isCvcValid !== null">
                {{ isCvcValid ? 'Valid security code' : 'Invalid security code' }}
            </div> 
        </div>
        <div v-if="paymentSuccess !== true" class = 'Container Four'>
            <button type="submit">PAY NOW</button>
        </div>
        </form>
    </div>
    <!-- FORM SUCESS -->
    <div v-else="showForm == false" id = 'paymentSucess'>
        <div class = 'Container Four Success' >
            PAYMENT SUCCESS 
        </div>
        <img src="https://iili.io/JIONbVI.png" alt="Payment Success Icon" />
    </div>
    </template>
    
<script setup>
    import { ref } from 'vue';
    import {
        isValid,
        isExpirationDateValid,
        isSecurityCodeValid,
        getCreditCardNameByNumber,
    } from 'creditcard.js';
    
    const creditCardNumber = ref(null);
    const isCreditCardValid = ref(null);
    const creditCardName = ref(null);
    const expiry = ref(null);
    const isExpirationValid = ref(null);
    const cvc = ref(null);
    const isCvcValid = ref(null);
    const paymentSuccess = ref(null);

    const checkCreditCardValidity = () => {
    const numericCreditCardNumber = creditCardNumber.value.replace(/\D/g, '');
    try {
        creditCardName.value = getCreditCardNameByNumber(numericCreditCardNumber);
        if (!['Visa', 'Amex', 'Mastercard', 'Diners'].includes(creditCardName.value)) {
            throw new Error('Tipo de tarjeta no admitido');
        }
        if (numericCreditCardNumber.length >= 14) {
            isCreditCardValid.value = isValid(numericCreditCardNumber);
            creditCardNumber.value = numericCreditCardNumber.match(/.{1,4}/g).join('');
        } else {
            isCreditCardValid.value = null;
            creditCardName.value = null;
        }
    } catch (error) {
        console.error(error.message);
        // Puedes manejar el error de la forma que prefieras, por ejemplo, mostrar un mensaje al usuario.
        // También podrías establecer creditCardName.value en null para indicar que no es una tarjeta admitida.
        creditCardName.value = null;
        isCreditCardValid.value = false;
    }
    };

    const validateExpirationDate = () => {
                const [month, year] = expiry.value.split('/');
                isExpirationValid.value = isExpirationDateValid(month, `20${year}`);
            };
            const validateCvc = () => {
                isCvcValid.value = isSecurityCodeValid(creditCardNumber.value, cvc.value);
            };
    
    const showForm = ref(true);  // Variable de estado para controlar la renderización del formulario
    
    const processPayment = () => {
      // Lógica de procesamiento de pago
        if (isCreditCardValid.value && isExpirationValid.value && isCvcValid.value) {
        // Aquí puedes agregar la lógica para procesar el pago
        console.log('Pago realizado');
        // Cambia el valor de showForm para que el formulario no se renderice después de realizar el pago
        showForm.value = false;
        } else {
        console.log('Formulario inválido, corrija los errores antes de enviar.');
        }
    };
    </script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Poppins');
/* Ahora funciona Poppins en este apartado */
    .Container{
        width: 446px;
        height: 104px;
        flex-shrink: 0;
        
        margin-bottom: 35px;
        *{
            display: block;
        }
    }
    .Container label{
        /* Input Label (Card Number) */
        width: 212px;
        height: 26px;
        flex-shrink: 0;
        margin-bottom: 14px;
        color: #363537;
        color: rgba(54, 53, 55, 0.76);
        font-family: 'Poppins', sans-serif;
        font-size: 21px;
        font-style: normal;
        font-weight: 500;
        line-height: normal;
    }

    .Container input{
        width: 446px;
        height: 64px;
        flex-shrink: 0;
        fill: #e5e5e5;

        box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25) inset;

        background: hsl(0, 0%, 90%);
        border: none;
        border-radius: 10px;

        /* Ubicar texto en el centro */
        padding-left: 11px;
        padding-top: 15px;
        padding-bottom: 23px;
        padding-right: 90px;

    }
    .Container.First input{
        width: 446px;
    }
    .Container.Third input{
        width: 446px;
        height: 64px;
        flex-shrink: 0;
        fill: #E5E5E5;
        box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25) inset;
    }

    .Container.Four {
        width: 100%;
        height: 61px;
        flex-shrink: 0;
        display: grid;
        place-items: center;
    }
    .Container.Four button{
        width: 378px;
        height: 61px;
        border-radius: 10px;
        background: #546DEF;
        box-shadow: 4px 4px 10px 0px rgba(0, 0, 0, 0.25);
        border:none;
        color: #FFF;
        font-family: Roboto;
        font-size: 30px;
        font-style: normal;
        font-weight: 700;
        line-height: normal;

        position: relative;
    }

    .Container.Four button:hover{
        width: 378px;
        height: 61px;
        border-radius: 10px;
        background: #3d50af;
        box-shadow: 4px 4px 10px 0px rgba(0, 0, 0, 0.25);
        border:none;
        color: #FFF;
        font-family: Roboto;
        font-size: 30px;
        font-style: normal;
        font-weight: 700;
        line-height: normal;
        transition: 0.3s;
    }

    .Container.Four.Success button{
        background: greenyellow;
    }
    .Container.Four.Success button:hover{
        background: rgb(255, 47, 203);
    }
    div.Container > input{
        color: rgba(54, 53, 55, 0.76);
        font-family: Poppins;
        font-size: 21px;
        font-style: normal;
        font-weight: 500;
        line-height: normal;

        position: relative;
    }

    div.Container.First > img{
        width: 40px;
        position:relative;
    }

    div.Container input:hover {
        background: white;
        transition: 0.3s;
    }

    .logoCard > img {
        width: 73px;
        height: 44px;
        flex-shrink: 0;
        position: absolute;
        right: 100px;
        transform: translateY(25%);
        border-radius: 7px;
    }

    .Container .Four .Sucess{
        color: #363537;
        font-family: Roboto;
        font-size: 36px;
        font-style: normal;
        font-weight: 700;
        line-height: normal;
    }

    #paymentSucess > img {
        position: absolute;
        z-index: 2;
        left: 358px;
    }

    #paymentSucess > div{
        color: #363537;
        font-family: Roboto;
        font-size: 36px;
        font-style: normal;
        font-weight: 700;
        line-height: normal;
        position: absolute;
        left: 18%;
        color: rgb(9, 124, 57);
        font-size: 42px;
    }

    form > * {
        position: relative;
    }

    .logoCard{
        position: absolute;
        z-index: 2;
        right: -90px;
    }
    
</style>
