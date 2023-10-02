<template>
    <div class="container">
        <ul>
            <li v-for="item in bookList" :key="item.id">
                <span>书名：{{ item.name }}</span>
                <span>作者：{{ item.author }}</span>
                <button @click="delBook(item.id)">删除</button>
            </li>
        </ul>
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
        },
    }
</script>

<style></style>
