<template>
    <div class="container">
        <table>
            <thead>
                <tr>
                    <th>编号</th>
                    <th>选中</th>
                    <th>数量</th>
                    <th>价格</th>
                    <th>小计</th>
                    <th>操作</th>
                </tr>
            </thead>
            <tbody v-if="list.length">
                <tr v-for="item in list" :key="item.id">
                    <td>{{ item.id }}</td>
                    <td><input type="checkbox" name="" id="" v-model="item.isChecked" /></td>
                    <td>
                        <button :disabled="item.num <= 1" @click="item.num--">-</button>
                        <span>{{ item.num }}</span>
                        <button @click="item.num++">+</button>
                    </td>
                    <td>
                        <input type="text" v-model="item.price" />
                    </td>
                    <td>{{ item.num * item.price }}</td>
                    <td><button @click="delItem(item.id)">删除</button></td>
                </tr>
            </tbody>
            <tbody v-if="!list.length">暂无数据</tbody>
            <tfoot>
                <input type="checkbox" v-model="isAll" />
                全选
                <div>总计：{{ calTotal }}</div>
                <button>结算（{{ calCount }}）</button>
            </tfoot>
        </table>
    </div>
</template>

<script>
    const defaultArr = [
        { id: 1, isChecked: true, num: 2, price: 6 },
        { id: 2, isChecked: false, num: 1, price: 8 },
        { id: 3, isChecked: true, num: 3, price: 3 },
        { id: 4, isChecked: true, num: 4, price: 2 },
        { id: 5, isChecked: true, num: 7, price: 8 },
    ]
    export default {
        data: () => {
            return {
                list: JSON.parse(localStorage.getItem("list")) || defaultArr,
            }
        },
        computed: {
            calTotal() {
                return this.list.reduce((sum, item) => {
                    if (item.isChecked === true) {
                        sum += Number(item.num) * Number(item.price)
                    }
                    return sum
                }, 0)
            },
            calCount() {
                return this.list.reduce((sum, item) => {
                    if (item.isChecked === true) {
                        sum += Number(item.num)
                    }
                    return sum
                }, 0)
            },
            isAll: {
                // 这里要做特殊处理
                get() {
                    return this.list.every(item => item.isChecked)
                },
                set(value) {
                    this.list.forEach(item => (item.isChecked = value))
                },
            },
        },
        watch: {
            list: {
                deep: true,
                handler(newValue) {
                    // 需要将其存在本地
                    localStorage.setItem("list", JSON.stringify(newValue))
                },
            },
        },
        methods: {
            delItem(id) {
                this.list = this.list.filter(item => item.id !== id)
            },
            delAll() {
                this.list = []
            },
        },
    }
</script>

<style></style>
