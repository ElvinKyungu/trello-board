<script setup lang="ts">
import type { Column } from '~~/types'
import { nanoid } from 'nanoid'
import draggable from 'vuedraggable';

const columns = ref<Column[]>([
    {
        id: nanoid(),
        title: "Backlog",
        tasks: [
            {
                title: "Create marketing landing page",
                createdAt: new Date(),
                id: nanoid(),
            },
            {
                title: "Fix page nav bug",
                createdAt: new Date(),
                id: nanoid(),
            },
            {
                title: "Develop cool new feature",
                createdAt: new Date(),
                id: nanoid(),
            }
        ],
    },
    { title: "Selected for dev", id: nanoid(), tasks: [] },
    { title: "In progress", id: nanoid(), tasks: [] },
    { title: "QA", id: nanoid(), tasks: [] },
    { title: "Complete", id: nanoid(), tasks: [] }
]);
</script>

<template>
    <div>
        <div >
            <draggable
                v-model="columns"
                group-key="columns"
                item-key="id"
                animation="150"
                handle=".draggble"
                class="flex gap-4 overflow-x-auto items-start"
            >
                <template #item="{element: column } : {element: Column}">
                    <div class="column bg-gray-200 p-5 rounded min-w-[250px]">
                        <header class="font-bold mb-4 flex items-center gap-2">
                            <span class="draggble cursor-move">
                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-grip-vertical" viewBox="0 0 16 16">
                                    <path d="M7 2a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm3 0a1 1 0 1 1-2 0 1 1 0 0 1 2 0zM7 5a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm3 0a1 1 0 1 1-2 0 1 1 0 0 1 2 0zM7 8a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm3 0a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm-3 3a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm3 0a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm-3 3a1 1 0 1 1-2 0 1 1 0 0 1 2 0zm3 0a1 1 0 1 1-2 0 1 1 0 0 1 2 0z"/>
                                </svg>
                            </span>
                            {{ column.title }}
                        </header>
                        <TrelloBoardTask 
                            v-for="task in column.tasks"
                            :key="task.id"
                            :task="task"
                        />
                        <footer>
                            <button class="text-gray-500">+ Add a card</button>
                        </footer>
                    </div>
                </template>
            </draggable>
        </div>
    </div>
</template>

