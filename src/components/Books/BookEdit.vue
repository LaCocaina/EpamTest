<template>
    <div class="book-edit">
        <div v-if="error" class="notification notification__error" @click="error = 0">Что-то не так...</div>
        <div class="book-edit__input">
            <div class="book-edit__l book-edit__l-label"><img v-if="b.pic" :src="b.pic"></div>
            <div class="book-edit__l book-edit__l-input"><input type="text" v-model="b.pic" placeholder="Ссылка на изображение"></div>
        </div>
        <div class="book-edit__input">
            <div class="book-edit__l book-edit__l-label"></div><div class="book-edit__l book-edit__l-input"><input type="text" v-model="b.name" placeholder="Название книги"></div>
        </div>
        <div class="book-edit__input">
            <div class="book-edit__l book-edit__l-label"></div><div class="book-edit__l book-edit__l-input"><input type="text" v-model="b.author" placeholder="Имя автора"></div>
        </div>
        <div class="book-edit__input">
            <div class="book-edit__l book-edit__l-label"></div><div class="book-edit__l book-edit__l-input"><input type="text" v-model.number="b.year" placeholder="Год выпуска книги"></div>
        </div>
        <div class="book-edit__input book-edit__buttons">
            <Button v-if="changed" :type="'whi'" @click.native="reset">Восстановить</Button> <Button :type="'add'" @click.native="save">Сохранить</Button>
        </div>
    </div>
</template>

<script>
    import Button from "@/components/Button";
    export default {
        name: "BookEdit",
        components: {Button},
        props: ['book'],
        data() {
            return {
                error: 0,
                b: {},
                changed: 1,
            }
        },
        methods: {
            save() {
                if (this.checkLink(this.b.pic) && this.checkYear(this.b.year) && (this.b.name && this.b.author)) {
                    this.$emit('saveBook', this.b);
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
            },
            reset() {
                this.b = Object.assign({}, this.book);
            },
        },
        mounted() {
            this.reset();
        }
    }
</script>

<style scoped>
    .book-edit {
        display: flex;
        flex-direction: column;
        padding: 20px;
        border: 1px dashed #ccc;
        border-radius: 5px;
        margin-bottom: 10px;
    }
    .book-edit__input {
        display: flex;
        padding: 5px 0;
    }
    .book-edit__l {
        display: flex;
        position: relative;
    }
    .book-edit__l.book-edit__l-input {
        width: 100%;
    }
    .book-edit__l.book-edit__l-label {
        flex: 0 0 150px;
        margin-right: 15px;
    }
    .book-edit__l.book-edit__l-label > img {
        max-width: 150px;
        position: absolute;
        top: 0;
        left: 0;
    }
    .book-edit__input.book-edit__buttons {
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
    .book-edit__l.book-edit__l-input > input {
        border: none;
        border-bottom: 2px solid #ccc;
        padding: 5px 0;
        width: 100%;
    }
</style>