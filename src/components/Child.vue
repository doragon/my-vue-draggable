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
    watch: {
        listFromParent: function (newlist, oldlist) {
            if (!(newlist instanceof Array) || !(oldlist instanceof Array)) {
                return;
            }
            this.list3 = this.listFromParent.filter((task) => {
                const lastword = task.slice(-1);
                return lastword === '1' || lastword === '2';
            });
            this.list4 = this.listFromParent.filter((task) => {
                const lastword = task.slice(-1);
                return lastword === '3' || lastword === '4';
            });
        },
        list3: function (newlist, oldlist) {
            if (!(newlist instanceof Array) || !(oldlist instanceof Array)) {
                return;
            }
            if (newlist.length === oldlist.length) {
                return;
            }
            this.$emit('update', newlist.concat(this.list4));
        },
        list4: function (newlist, oldlist) {
            if (!(newlist instanceof Array) || !(oldlist instanceof Array)) {
                return;
            }
            if (newlist.length === oldlist.length) {
                return;
            }
            this.$emit('update', newlist.concat(this.list3));
        },
    },
    data: ()=> {
        return {
            list3: [],
            list4: [],
        }
    },
}
</script>
