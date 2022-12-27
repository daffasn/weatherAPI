<template>
    <div class="frontloading">
        <div class="customloading">
            <div class="lds-ring">
                <div></div>
                <div></div>
                <div></div>
                <div></div>
            </div>
            <h3>Loading</h3>
        </div>
    </div>
</template>

<style scoped>
        .customloading > .lds-ring {
            position: relative;
            top: -40px;
            left: -50px;
        }
        .customloading > h3 {
            position: relative;
            top: -50px;
            left: 15px;
        }
        .frontloading {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .lds-ring {
        display: inline-block;
        position: relative;
        width: 80px;
        height: 80px;
        }
        .lds-ring div {
        box-sizing: border-box;
        display: block;
        position: absolute;
        width: 164px;
        height: 164px;
        margin: 8px;
        border: 16px solid #000;
        border-radius: 50%;
        animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
        border-color: #000 transparent transparent transparent;
        }
        .lds-ring div:nth-child(1) {
        animation-delay: -0.45s;
        }
        .lds-ring div:nth-child(2) {
        animation-delay: -0.3s;
        }
        .lds-ring div:nth-child(3) {
        animation-delay: -0.15s;
        }
        @keyframes lds-ring {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
        }
</style>