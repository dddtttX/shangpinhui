<template>
    <div class="list">
        <div class="item" v-for="item in list" :key="item.id">
            <div class="left">
                {{ item.id }}
                <input type="checkbox" v-model="item.isFinished" />
                <span>{{ item.todo }}</span>
            </div>
            <div class="right">
                {{ item.addTime }}
                <button @click="delItem(item.id)">删除</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: () => {
            return {}
        },
        methods: {
            delItem(id) {
                this.$emit("delItem", id)
            },
        },
        props: ["list"],
    }
</script>

<style lang="less">
    .list {
        flex: 1;
        width: 100%;
        margin: 5px;
        border: 1px solid grey;
        padding: 5px;
        overflow-y: scroll;
        .item {
            display: flex;
            margin: 5px;
            padding-left: 5px;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid grey;

            .left {
                display: flex;
                align-items: center;
            }
        }
    }
</style>
