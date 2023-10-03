<template>
    <div class="header">
        <input type="text" placeholder="请输入你的任务，按回车键确认" @keyup="keyAddHandler" ref="enterInput" />
    </div>
</template>

<script>
    const debounce = function (func, delay) {
        let timer = null
        return function (...args) {
            if (timer) clearTimeout(timer)
            timer = setTimeout(() => {
                func.apply(this, args)
            }, delay)
        }
    }
    export default {
        data: () => {
            return {
                timer: null,
            }
        },
        created() {},
        methods: {
            keyAddHandler: debounce(function (e) {
                let val = e.target.value
                if (val === "" || val.trim() === "") return
                this.$emit("addItem", val)
                this.$refs.enterInput.value = ""
            }, 500),
        },
    }
</script>

<style lang="less">
    .header {
        width: 290px;
        text-align: center;
        input {
            width: 100%;
        }
    }
</style>
