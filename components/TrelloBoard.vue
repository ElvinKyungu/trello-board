<template>
    <div class="flex gap-4 overflow-x-auto items-start">
        <div>
            <div v-for="column in columns" :key="column.id">
                <header>
                    {{ column.title }}
                </header>
                <p v-for="task in column.tasks" :key="task.id">
                    {{ task.title }}
                </p>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import type { Column } from '~~/types'
import { nanoid } from 'nanoid'

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
