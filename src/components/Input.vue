<template>
    <span>
        <input type="text" 
            placeholder="New task"
            v-model="value"
            @keyup.enter="addNewTask"
            maxlength="100">
        <button @click="addNewTask">+</button>
    </span>
</template>

<script>
    import Buzz from '@/buzz'
    export default {
        data() {
            return {
                id: 9,
                value: ''
            }
        },
        methods: {
            addNewTask() {
                if(!this.value)
                    return;
                let id = this.id++
                const task = {
                    id,
                    description: this.value,
                    done: false
                }
               this.value = ''
                Buzz.emitEvent('newTask', task)
            }
        }
    }
</script>

<style scoped>
    span {        
        width: 30vw;        
        margin: 15px;
        border: 1px solid #9c9ca3;
        border-radius: 5px;
        display: flex;
        flex-direction: row;
    }
    input, button {  
        color: #d0d0df;     
        padding: 10px;
        background-color: transparent;
        border: none;
        outline: none;
    }
    input {
        flex: 1;
        z-index: 0;
    }
    button {
        background-color: #1a69df;
    }
    
</style>
