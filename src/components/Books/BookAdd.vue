<template>
    <div v-if="toggle" class="book-add">
        <div v-if="error" class="notification notification__error" @click="error = 0">Что-то не так...</div>
        <div class="book-add__input">
            <div class="book-add__l book-add__l-label"><img v-if="book.pic" :src="book.pic"></div>
            <div class="book-add__l book-add__l-input"><input type="text" v-model="book.pic" placeholder="Ссылка на изображение"></div>
        </div>
        <div class="book-add__input">
            <div class="book-add__l book-add__l-label"></div><div class="book-add__l book-add__l-input"><input type="text" v-model="book.name" placeholder="Название книги"></div>
        </div>
        <div class="book-add__input">
            <div class="book-add__l book-add__l-label"></div><div class="book-add__l book-add__l-input"><input type="text" v-model="book.author" placeholder="Имя автора"></div>
        </div>
        <div class="book-add__input">
            <div class="book-add__l book-add__l-label"></div><div class="book-add__l book-add__l-input"><input type="text" v-model.number="book.year" placeholder="Год выпуска книги"></div>
        </div>
        <div class="book-add__input book-add__buttons">
            <Button :type="'add'" @click.native="add">Добавить</Button> <Button @click.native="toggle = !toggle" :type="'can'">Отмена</Button>
        </div>
    </div>
    <div v-else class="book-add book-add__open-form" @click="toggle = !toggle">Добавить книгу</div>
</template>

<script>
    import Button from "@/components/Button";
    export default {
        name: "BookAdd",
        components: {Button},
        data() {
            return {
                toggle: 0,
                error: 0,
                book: {
                    id: 0,
                    pic: "",
                    name: "",
                    author: "",
                    year: "",
                }
            }
        },
        methods: {
            add() {
                if (this.checkLink(this.book.pic) && this.checkYear(this.book.year) && (this.book.name && this.book.author)) {
                    this.$emit('addBook', this.book);
                    this.toggle = !this.toggle;
                    this.error = 0;
                } else {
                    this.error = 1;
                }
            },
            checkLink(y) {
                let pat = /(https?:\/\/.*\.(?:png|jpg))/i;
                return pat.test(y);
            },
            checkYear(y) {
                let pat = /^\d+$/;
                return pat.test(y) && y >= 0 && y <= 2020;
            }
        }
    }
</script>

<style scoped>
    .book-add {
        display: flex;
        flex-direction: column;
        padding: 15px;
        border: 1px dashed #ccc;
        border-radius: 5px;
        margin-bottom: 10px;
    }
    .book-add.book-add__open-form {
        color: #008fd8;
        text-decoration: underline;
        cursor: pointer;
    }
    .book-add__input {
        display: flex;
        padding: 5px 0;
    }
    .book-add__l {
        display: flex;
        position: relative;
    }
    .book-add__l.book-add__l-input {
        width: 100%;
    }
    .book-add__l.book-add__l-label {
        flex: 0 0 150px;
        margin-right: 15px;
    }
    .book-add__l.book-add__l-label > img {
        max-width: 150px;
        position: absolute;
        top: 0;
        left: 0;
    }
    .book-add__input.book-add__buttons {
        justify-content: flex-end;
        padding-top: 15px;
    }
    .notification {
        padding: 15px;
        border-radius: 5px;
        cursor: pointer;
        margin-bottom: 10px;
    }
    .notification__error {
        background: linear-gradient(36deg, #ff00b4, #ff6000);
        color: #fff;
    }
    .book-add__l.book-add__l-input > input {
        border: none;
        border-bottom: 2px solid #ccc;
        padding: 5px 0;
        width: 100%;
    }
</style>