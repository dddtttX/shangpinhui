<template>
    <div class="container">
        <img :src="list[index]" alt="" />
        <button v-on:click="index--">上一页</button>
        <button v-on:click="index++">下一页</button>
        {{ index }}
    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                list: [
                    require("../static/01.png"),
                    require("../static/02.jpg"),
                    require("../static/03.jpg"),
                    require("../static/04.jpg"),
                ],
                index: 0,
            }
        },
    }
</script>

<style></style>
