<template>
    <div class = 'icon'>
        
        <p>X</p>
        
    </div>
    
</template>

<style scoped>

    .icon p{

        height: 100%;
        width: 100%;

        display: flex;
        justify-content: center;
        align-items: center;

        color: #363537;

        font-family: Roboto;
        font-size: 18px;
        font-style: normal;
        font-weight: 400;
        line-height: normal;
        

        position: relative;
        top: -4px;
    }

    
    .icon {

        background-image: url('../../assets/icon.svg');
        background-size: contain;
        width: 56px;
        height: 56px;
        flex-shrink: 0;

        position: absolute;
        right: 0;
        transform: translate(22px, -26px);

        fill: #DDE1E4;
        stroke-width: 1px;
        stroke: #363537;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));

        
    }
    .icon-text {
        display: flex;
        align-items: center;
        justify-content: center;
        color: #363537;
        font-family: 'Roboto';
        font-size: 24px;
        font-style: normal;
        font-weight: 400;
        line-height: normal;
        

        
        }


</style>