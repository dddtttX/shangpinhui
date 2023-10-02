<template>
    <div class="container">
        <table>
            <thead>
                <tr>
                    <th>编号</th>
                    <th>科目</th>
                    <th>成绩</th>
                    <th>操作</th>
                </tr>
            </thead>
            <tbody v-if="list.length">
                <tr v-for="item in list" :key="item.id">
                    <td>{{ item.id }}</td>
                    <td>{{ item.project }}</td>
                    <td>{{ item.score }}</td>
                    <td><button @click="delItem(item.id)">删除</button></td>
                </tr>
            </tbody>
            <tbody v-if="!list.length">暂无数据</tbody>
            <tfoot>
                <div>总分：{{ calTotal }}</div>
                <div>平均分：{{ calAvg }}</div>
            </tfoot>
        </table>
        科目：
        <input type="text" ref="project" />
        成绩：
        <input type="text" ref="score" />
        <button @click="addItem">添加</button>
    </div>
</template>

<script>
    export default {
        data: () => {
            return {
                list: [
                    { id: 1, project: "语文", score: 100 },
                    { id: 2, project: "数学", score: 95 },
                    { id: 3, project: "体育", score: 98 },
                    { id: 4, project: "英语", score: 60 },
                ],
            }
        },
        methods: {
            delItem(id) {
                this.list = this.list.filter(item => item.id !== id)
            },
            delAll() {
                this.list = []
            },
            addItem() {
                let length = this.list.length
                let id = length === 0 ? 1 : this.list[length - 1].id + 1
                let project = this.$refs.project.value
                let score = this.$refs.score.value
                if (project === "") {
                    alert("请输入合法的科目")
                    return
                }
                if (score === "" || score > "100" || score < "0") {
                    alert("请输入合法的成绩")
                    return
                }
                this.list.push({
                    id,
                    project,
                    score,
                })
                this.$refs.project.value = ""
                this.$refs.score.value = ""
            },
        },
        computed: {
            calAvg() {
                let total = 0
                let avg = 0
                this.list.map(item => {
                    total += Number(item.score)
                })
                avg = total / this.list.length
                return avg
            },
            calTotal() {
                let total = 0
                this.list.map(item => {
                    total += Number(item.score)
                })
                return total
            },
        },
    }
</script>

<style></style>
