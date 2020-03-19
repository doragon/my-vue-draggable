<template>
    <div>
        <h3>list1を表示</h3>
        <draggable v-model="list1" :options="{ group: 'tasks' }" class="dev_flex dev_setting-area">
            <div class="dev_back" v-for="(item) in list1" :key="item">{{ item }}</div>
        </draggable>

        <h3>list2を表示</h3>
        <draggable v-model="list2" :options="{ group: 'tasks' }" class="dev_flex dev_setting-area">
            <div class="dev_back" v-for="(item) in list2" :key="item">{{ item }}</div>
        </draggable>

        <h3>listForChildを表示</h3>
        <Child :list-from-parent="listForChild" v-on:update="listForChild = $event;"></Child>
    </div>
</template>

<script>
import draggable from 'vuedraggable';

import Child from '@/components/Child.vue'

export default {
    name: "Parent",
    components: {
        draggable,
        Child
    },
    data: ()=> {
        return {
            list1: ['task1-1', 'task1-2', 'task1-3', 'task1-4'],
            list2: ['task2-1', 'task2-2', 'task2-3', 'task2-4'],
            listForChild: ['task3-1']
        }
    },
}
</script>

<style>
.dev_flex {
    display: flex;
}

.dev_setting-area {
    color: #fff;
    border: 6px double #fff;
    background: #464646;
    border-radius: 10px;
    margin: .5rem;
    padding: .5rem;
    height: 16mm;
}

.dev_back {
    margin: .1em;
    width: 15mm;
    height: 15mm;
    text-decoration: none;
    color: #67c5ff;
    border: solid 1px #67c5ff;
    border-radius: 3px;
    transition: .4s;
}
</style>