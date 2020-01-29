<template>
    <div id="books">
        <Book @saveBook="saveBook" @deleteBook="deleteBook" v-for="b in books" :key="b.id" :book="b"></Book>
        <BookAdd @addBook="addBook"></BookAdd>
    </div>
</template>

<script>
    import Book from "@/components/Books/Book";
    import BookAdd from "@/components/Books/BookAdd";
    export default {
        name: "Books",
        components: {BookAdd, Book},
        data() {
            return {
                books: [
                    {
                        id: 1,
                        pic: "https://img1.wbstatic.net/large/new/6410000/6411503-1.jpg",
                        author: "Дж. Ханк Рейнвотер",
                        name: "Как пасти котов",
                        year: 2011,
                    },
                    {
                        id: 2,
                        pic: "https://www.moscowbooks.ru/image/book/607/orig/i607672.jpg",
                        author: "Даниэль Дефо",
                        name: "Робинзон Крузо",
                        year: 1719,
                    }
                ],
            }
        },
        methods: {
            addBook(data) {
                let max = 0;
                this.books.map(
                    n => {
                        max = n.id > max ? n.id : max;
                    }
                );
                data.id = ++max;
                this.books.push(data);
            },
            deleteBook(id) {
                let del = this.books.map( n => { return n.id; })
                    .indexOf(id);

                del >= 0 && this.books.splice(del, 1);
            },
            saveBook(data) {
                let sav = this.books.map( n => { return n.id; })
                    .indexOf(data.id);
                this.$set(this.books, sav, data);
            }
        }
    }
</script>

<style scoped>
    #books {
        max-width: 700px;
        width: 100%;
        margin: 0 auto;
    }
</style>