<script setup lang="ts">
import { ref } from "vue";
import { Todolist, TodoForm } from '../types'

const todoList = ref<Todolist[]>([
    {
        title: 'Teest',
        description: 'Teest',
        isComplete: false
    },
    {
        title: 'Teest',
        description: 'Teest',
        isComplete: false
    }
]);

const todoListForm = ref({} as TodoForm)

const handleAddTodo = () => {
    todoList.value.push({ ...todoListForm.value, isComplete: false })
    todoListForm.value = {} as TodoForm
}

const handleRemoveTodo = (todoIndex: number): void => {
    todoList.value = todoList.value.filter((todo, index) => index !== todoIndex)
}

const handleCompleteTodo = (todoIndex: number): void => {
    todoList.value = todoList.value.map((todo, index) => {
        if (index !== todoIndex) {
            return todo
        }

        return { ...todo, isComplete: !todo.isComplete }
    })
}

</script>

<template>
    <div class="min-h-screen flex-col flex">
        <header class="h-16 bg-green-300 mb-2 flex items-center">
            <h1 class="text-2xl"><b>TodoList</b></h1>
        </header>
        <main class="flex-1">
            <div class="w-1/2 m-auto mb-4 bg-green-300 p-4">
                <form @submit.prevent="handleAddTodo">
                    <input
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        id="title" type="text" placeholder="Title" v-model="todoListForm.title" required>
                    <textarea v-model="todoListForm.description" id="description" name="description" rows="10" cols="10"
                        class="mt-1 py-2 px-3 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
                        placeholder="Description" required></textarea>
                    <button
                        class="mt-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                        type="submit">
                        Submit
                    </button>
                </form>
            </div>
            <div class="flex gap-4 flex-wrap justify-center">
                <div class="bg-green-300 w-96 h-48 p-2 overflow-auto" v-for="(todo, index) in todoList" :key="index">
                    <div class="flex justify-between items-center mb-2">
                        <button
                            class="mt-2 mr-1 bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                            @click="handleCompleteTodo(index)">
                            {{ !todo.isComplete ? 'Done' : 'To do' }}
                        </button>
                        <button
                            class="mt-2 ml-1 bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                            @click="handleRemoveTodo(index)">
                            remove
                        </button>
                    </div>
                    <div class="flex justify-between">
                        <label class="text-xl">{{ todo.title }}</label>
                        <label>{{ todo.isComplete ? 'Done' : 'In-progress' }}</label>
                    </div>
                    <p class="mt-4">{{ todo.description }}</p>
                </div>
            </div>
        </main>
    </div>
</template>

<style>

</style>