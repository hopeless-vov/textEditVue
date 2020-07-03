<template>
    <form @submit.prevent ="onSubmit">
        <input type="text" v-model="title">
        <button type="sumbit">Create</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title:''
        }
    },
    methods: {
        onSubmit() {
            console.log('Sumbit', this.title)
            if (this.title.trim()) {
                const newTodo ={
                    id:Date.now(),
                    title:this.title,
                    completed:false
                }
                
                this.$emit('add-todo', newTodo),
                this.title = ''
            }
        }
    }
}
</script>
<style>
form {
    display:flex;
    margin: 10px;
}
 
</style>