<script lang="ts">
interface ToDo {
    task: string;
    completed: boolean;
    focused: boolean;
}

export default {
    name: "ToDo",
    data: function () {
        return {
            todos: [],
            todoText: '',
        }
    },
    methods: {
        addTodo: function () {
            (this.todos as ToDo[]) = [...this.todos, {
                    task: this.todoText as string,
                    completed: false,
                    focused: false
                } as ToDo
            ];
            localStorage.setItem('todos', JSON.stringify(this.todos));
            this.todoText = '';
        },
        removeTodo: function (index: number) {
            (this.todos as ToDo[]).splice(index, 1);
            localStorage.setItem('todos', JSON.stringify(this.todos));
        },
        completeTodo: function (index: number) {
            // add class
            (this.todos as ToDo[])[index].completed = !(this.todos as ToDo[])[index].completed;
            localStorage.setItem('todos', JSON.stringify(this.todos));
        },
    },
    mounted: function () {
        if (localStorage.getItem('todos')) {
            this.todos = JSON.parse(localStorage.getItem('todos') as string);
        } else {
            this.todos = [];
        }
    }
}
</script>

<template>
<div class="absolute bottom-10 left-10 text-white">
    <div class="mb-5">
        <ul class="text-white">
            <li v-for="(todo, index) in todos" :key="index" class="group flex flex-row justify-between items-center
                    border border-solid border-white rounded-md 
                    px-2 py-1 my-2">
                <div class="flex flex-row justify-center items-center">
                    <div class="w-4 h-4 
                        border-white border border-solid 
                        mr-3 rounded-full
                        cursor-pointer" 
                        @click="() => completeTodo(index)">
                        <span v-if="(todo as ToDo).completed" class="translate-x-[2px] -translate-y-2 absolute select-none">✓</span>
                    </div>
                    <div :class="{'line-through' : (todo as ToDo).completed}">{{ (todo as ToDo).task }}</div>
                </div>
                <div @click="() => removeTodo(index)" class="hidden group-hover:block cursor-pointer">🗑️</div>
            </li>
        </ul>
    </div>

    <form v-on:submit.prevent="addTodo">
        <input v-model="todoText" type="text" placeholder="To Do" class="bg-gray-600 px-2 py-1 rounded-md">
        <button type="submit" class="bg-gray-500 px-3 pb-1 ml-1 rounded-md text-center text-xl">+</button>
    </form>
</div>
</template>
