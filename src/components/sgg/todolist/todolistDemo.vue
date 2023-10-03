<template>
    <div class="todoList">
        <h1>小黑记事本</h1>
        <HeaderVue @addItem="addItem"></HeaderVue>
        <ListVue :list="list" @delItem="delItem"></ListVue>
        <FooterVue
            :isFinishedCount="isFinishedCount"
            :total="total"
            @changeIsAllBox="changeIsAll"
            @delFinishedItems="delFinishedItems"
        ></FooterVue>
    </div>
</template>

<script>
    import HeaderVue from "./components/HeaderVue.vue"
    import FooterVue from "./components/FooterVue.vue"
    import ListVue from "./components/ListVue.vue"

    const defaultArr = [
        { id: 5, todo: "事项5", isFinished: true, addTime: new Date().toLocaleDateString() },
        { id: 4, todo: "事项4", isFinished: false, addTime: new Date().toLocaleDateString() },
        { id: 3, todo: "事项3", isFinished: true, addTime: new Date().toLocaleDateString() },
        { id: 2, todo: "事项2", isFinished: false, addTime: new Date().toLocaleDateString() },
        { id: 1, todo: "事项1", isFinished: true, addTime: new Date().toLocaleDateString() },
    ]
    export default {
        data: () => {
            return {
                list: JSON.parse(localStorage.getItem("list")) || defaultArr,
            }
        },
        computed: {
            total() {
                return this.list.length
            },
            isFinishedCount() {
                return this.list.reduce((count, item) => {
                    if (item.isFinished) {
                        return count + 1
                    } else {
                        return count
                    }
                }, 0)
            },
        },
        methods: {
            changeIsAll(curState) {
                this.list.forEach(item => {
                    item.isFinished = curState
                })
            },
            addItem(todo) {
                let length = this.list.length
                if (this.list.find(item => todo === item.todo)) {
                    alert("请勿重复添加")
                    return
                }

                this.list.unshift({
                    id: length ? this.list[0].id + 1 : 1,
                    todo,
                    isFinished: false,
                    addTime: new Date().toLocaleDateString(),
                })
            },
            delItem(id) {
                this.list = this.list.filter(item => item.id !== id)
            },
            delFinishedItems() {
                this.list = this.list.filter(item => !item.isFinished)
            },
        },

        watch: {
            list: {
                deep: true,
                handler() {
                    localStorage.setItem("list", JSON.stringify(this.list))
                },
            },
        },

        components: {
            HeaderVue,
            FooterVue,
            ListVue,
        },
    }
</script>

<style scoped>
    .todoList {
        margin: 20px auto;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 400px;
        height: 500px;
        padding: 5px;
        border: 1px solid grey;
    }
</style>
>
