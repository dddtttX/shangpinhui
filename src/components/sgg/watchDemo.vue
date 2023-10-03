<template>
    <div class="container">
        <h2>今天天气很{{ getInfo }}</h2>
        <button @click="isHot = !isHot">切换天气</button>
        <div>{{ numbers.a }}</div>
        <button @click="numbers.a++">点我让a加1</button>
    </div>
</template>

<script>
    export default {
        data: () => {
            return {
                isHot: false,
                numbers: {
                    a: 1,
                    b: 2,
                },
            }
        },
        watch: {
            // 计算属性也可以监视
            getInfo: {
                handler(newValue, oldValue) {
                    console.log(newValue)
                    console.log(oldValue)
                },
            },
            // 深度监视写法一
            "numbers.a": {
                // handler(nv) {
                // console.log(nv)
                // },
            },
            // 深度监视写法二
            numbers: {
                deep: true,
                handler(nv) {
                    console.log(nv)
                },
            },
        },
        computed: {
            getInfo() {
                return this.isHot ? "冷" : "热"
            },
        },
    }
</script>

<style></style>
