<template>
    <div class="book-wrapper">
        <div class="book">
            <div class="book-block">
                <div class="book-block__image">
                    <img :src="book.pic">
                </div>
            </div>
            <div class="book-block book-block__info">
                <div class="book-line book-line__name">{{ book.name }}</div>
                <div class="book-line book-line__author">{{ book.author }}</div>
                <div class="book-line book-line__year">{{ book.year }} г.</div>
            </div>
            <div class="book-block book-block__opt">
                <Button v-if="!toggleEdit" @click.native="toggleEdit = !toggleEdit" :type="'add'">Изменить</Button>
                <Button @click.native="$emit('deleteBook', book.id)" :type="'can'">Удалить</Button>
            </div>
        </div>
        <div v-if="toggleEdit" class="book__edit">
            <BookEdit @saveBook="saveBook" :book="book"></BookEdit>
        </div>
    </div>
</template>

<script>
    import Button from "@/components/Button";
    import BookEdit from "@/components/Books/BookEdit";
    export default {
        name: "Book",
        components: {BookEdit, Button},
        props: ["book"],
        data() {
            return {
                toggleEdit: 0,
            }
        },
        methods: {
            saveBook(data) {
                this.$emit('saveBook', data);
                this.toggleEdit = !this.toggleEdit;
            }
        }
    }
</script>

<style scoped>
    .book {
        display: flex;
        border: 1px solid #ccc;
        border-radius: 5px;
        margin-bottom: 10px;
    }
    .book-block {
        display: flex;
    }
    .book-block > .book-block__image {
        display: flex;
        justify-content: center;
    }
    .book-block .book-block__image img {
        max-height: auto;
        max-width: 150px;
        border-radius: 5px 0 0 5px;
    }
    .book-block.book-block__info {
        justify-content: center;
        flex-direction: column;
        padding: 15px;
        width: 100%;
    }
    .book-block__opt {
        align-items: center;
        padding: 20px;
    }
    .book-line__name {
        font-size: 23px;
        font-weight: 800;
    }
    .book-line__year {
        color: #999;
    }
</style>