<template>
    <div class="SellMachine">
        <div class="container">
            小黑自动售货机
            <button v-on:click="buy(5)">可乐5元</button>
            <button @click="buy(10)">咖啡10元</button>
        </div>
        <div class="left">银行卡剩余：{{ account }}</div>
    </div>
</template>

<script>
    export default {
        data: () => {
            return {
                account: 1000,
            }
        },
        methods: {
            buy(money) {
                this.account -= money
            },
        },
    }
</script>

<style></style>
