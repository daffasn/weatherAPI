<template>
    <div class="thridloading">
        <div class="lds-facebook"><div></div><div></div><div></div></div>
        <span>The content is loading...</span>
    </div>
</template>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Righteous&display=swap');
    
        .thridloading {
            height: 90vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            font-family: 'Righteous', cursive;
            font-size: 20px;
        }
        .lds-facebook {
        display: inline-block;
        position: relative;
        width: 80px;
        height: 200px;
        }
        .lds-facebook div {
        display: inline-block;
        position: absolute;
        left: 8px;
        width: 76px;
        background: #000;
        animation: lds-facebook 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
        }
        .lds-facebook div:nth-child(1) {
        left: -100px;
        animation-delay: -0.44s;
        }
        .lds-facebook div:nth-child(2) {
        left: 6px;
        animation-delay: -0.22s;
        }
        .lds-facebook div:nth-child(3) {
        left: 116px;
        animation-delay: 0;
        }
        @keyframes lds-facebook {
        0% {
            top: 2px;
            height: 200px;
        }
        50%, 100% {
            top: 56px;
            height: 52px;
        }
        }
</style>