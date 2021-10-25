<template>
    <div>
        <h2 class="title">My list</h2>
        <div v-for="(item, index) in items"  v-bind:key="index">
            <tasks  class="item" :item="item" v-on:taskChanged="$emit('reloadList')" />
        </div>
    </div>
</template>

<script>
import Tasks from './Tasks.vue'
export default {
    props:['items'],
    components: {
        Tasks
    }
}
</script>

<style scoped>
.item{
    background: #e6e6e6;
    padding:5px;
    margin-top: 5px;
}
</style>