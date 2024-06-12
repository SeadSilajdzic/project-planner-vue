<script>
export default {
    name: "FilterNav",
    props: ['current'],
    methods: {
        updateFilter(by) {
            this.$emit("filterChange", by);
        }
    }
}
</script>

<template>
    <nav class="filter-nav">
        <button @click="updateFilter('all')" :class="{active: current === 'all'}">View all</button>
        <button @click="updateFilter('completed')" :class="{active: current === 'completed'}">Completed</button>
        <button @click="updateFilter('uncompleted')" :class="{active: current === 'uncompleted'}">Uncompleted</button>
    </nav>
</template>

<style scoped>
.filter-nav {
    display: flex;
    align-items: center;
    justify-content: center;
}

.filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    cursor: pointer;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
}

.filter-nav button.active {
    color: #555;
}
</style>