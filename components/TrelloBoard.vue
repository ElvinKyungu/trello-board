<script setup lang="ts">
import type { Column, Task } from '~~/types'
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
                group="columns"
                item-key="id"
                :animation="150"
                handle=".draggble-handle"
                class="flex gap-4 overflow-x-auto items-start"
            >
                <template #item="{element: column } : {element: Column}">
                    <div class="column bg-gray-200 p-5 rounded min-w-[250px]">
                        <header class="font-bold mb-4 flex items-center gap-2">
                            <DragHandle/>
                            {{ column.title }}
                        </header>
                        <draggable
                            v-model="column.tasks"
                            group="tasks"
                            item-key="id"
                            :animation="150"
                        >
                            <template #item="{ element: task }: { element: Task }">
                                <TrelloBoardTask
                                    :task="task"
                                />
                            </template>
                        </draggable>
                        <footer>
                            <button class="text-gray-500">+ Add a card</button>
                        </footer>
                    </div>
                </template>
            </draggable>
        </div>
    </div>
</template>

