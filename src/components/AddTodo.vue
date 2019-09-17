<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add Todo" />
            <button type="submit">ADD</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: "AddTodo",
        data() {
            return {
                title: ''
            }
        },
        methods: {
            addTodo(e) {
                e.preventDefault();
                const newTodo = {
                    title: this.title,
                    completed: false
                }

                this.$emit('add-todo', newTodo);

                this.title = '';
            }
        }
    }
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    button {
        flex: 2;
    }
</style>