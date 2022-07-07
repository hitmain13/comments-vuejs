<template>
    <div class="container">
        <FormTodo v-on:add-todo="addComment"></FormTodo>
        <h2>Comentários</h2>
        <p v-if="comments.length <= 0">Sem comentários...</p>
        <div class="list-group">
            <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
                <span class="comment__author">Autor: <strong>{{ comment.name }}</strong></span>
                <p>{{ comment.message }}</p>
                <div>
                    <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import FormTodo from './FormTodo.vue'

export default {
    name: "Form",
    components: {
        FormTodo
    },

    data() {
        return {
            comments: [],
        }
    },
    methods: {
        addComment(comment) {
            this.comments.push(comment);
        },
        removeComment(index) {
            this.comments.splice(index, 1);
        }
    },
    computed: {
        allComments() {
            return this.comments.map((comment) => ({
                ...comment,
                name: comment.name.trim() === '' ? '<Anônimo>' : comment.name
            }))
        }
    },
    watch: {
        comments(val) {
            console.log('val', val);
        }
    }
}
</script>