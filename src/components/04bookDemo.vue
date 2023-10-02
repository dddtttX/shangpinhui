<template>
    <div class="container">
        <div class="top">
            书名：
            <input type="text" ref="name" />
            作者：
            <input type="text" ref="author" />
            <button @click="addBook">添加书</button>
        </div>
        <div class="list">
            <ul class="container">
                <li v-for="item in bookList" :key="item.id">
                    <span>ID:{{ item.id }}</span>
                    <span>书名:{{ item.name }}</span>
                    <span>作者:{{ item.author }}</span>
                    <button @click="delBook(item.id)">删除</button>
                </li>
            </ul>
            <div class="bottom">
                <div class="count">合计：{{ bookList.length }}</div>
                <button @click="delAll">删除所有</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: () => {
            return {
                bookList: [
                    { id: 1, name: "《红楼梦》", author: "曹雪芹" },
                    { id: 2, name: "《三国演义》", author: "罗贯中" },
                    { id: 3, name: "《水浒传》", author: "施耐庵" },
                    { id: 4, name: "《西游记》", author: "吴承恩" },
                ],
            }
        },
        methods: {
            delBook(id) {
                this.bookList = this.bookList.filter(item => item.id !== id)
            },
            delAll() {
                this.bookList = []
            },
            addBook() {
                let length = this.bookList.length
                let id = length === 0 ? 1 : this.bookList[length - 1].id + 1
                console.log(id)
                let name = this.$refs.name.value
                let author = this.$refs.author.value
                if (name === "") {
                    alert("请输入合法的书名")
                    return
                }
                if (author === "") {
                    alert("请输入合法的作者名")
                    return
                }
                this.bookList.push({
                    id,
                    name: `《${name}》`,
                    author,
                })
                this.$refs.name.value = ""
                this.$refs.author.value = ""
            },
        },
    }
</script>

<style></style>
