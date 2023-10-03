<template>
    <div class="footer">
        <span>
            <input type="checkbox" name="" id="" v-model="isAll" />
            全选
        </span>
        <div>
            <span>已完成{{ isFinishedCount }}/全部{{ total }}</span>
        </div>
        <span>
            <button @click="delFinishedItems">删除已完成</button>
        </span>
    </div>
</template>

<script>
    export default {
        props: ["isFinishedCount", "total"],
        computed: {
            isAll: {
                get() {
                    return this.isFinishedCount == this.total && this.total !== 0
                },
                set(curState) {
                    this.$emit("changeIsAllBox", curState)
                },
            },
        },
        methods: {
            delFinishedItems() {
                this.$emit("delFinishedItems")
            },
        },
    }
</script>

<style>
    .footer {
        width: 90%;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>
