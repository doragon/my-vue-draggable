<template>
    <div>
        <h4>list3を表示</h4>
        <draggable v-model="list3" :options="{ group: 'tasks' }" class="dev_flex dev_setting-area">
            <div class="dev_back" v-for="(item) in list3" :key="item">{{ item }}</div>
        </draggable>

        <h4>list4を表示</h4>
        <draggable v-model="list4" :options="{ group: 'tasks' }" class="dev_flex dev_setting-area">
            <div class="dev_back" v-for="(item) in list4" :key="item">{{ item }}</div>
        </draggable>
    </div>
</template>

<script>
import draggable from 'vuedraggable';

export default {
    name: "Child",
    components: {
        draggable,
    },
    props: ['listFromParent'],
    computed: {
        list3: {
            get: function () {
                return this.listFromParent.concat().filter((task)=>{
                    const lastword = task.slice(-1);
                    return lastword === '1' || lastword === '2';
                });
            },
            set: function (list) {
                this.$emit('update', this.list4.concat(list));
            }
        },
        list4: {
            get: function () {
                return this.listFromParent.concat().filter((task)=>{
                    const lastword = task.slice(-1);
                    return lastword === '3' || lastword === '4';
                });
            },
            set: function (list) {
                this.$emit('update', this.list3.concat(list));
            }
        },
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