<template>
    <div class="clearAllContainer">
        <span class="clearAllBtn" @click="clearTodo">Clear All-test2</span>
    </div>
</template>

<script>
export default {
    methods: {
        clearTodo: function() {
            localStorage.clear();
        }
    }
}
</script>

<style scoped>
.clearAllContainer{
    width: 8.5rem;
    height: 50px;
    background-color: white;
    border-radius: 5px;
    margin: 0 auto;
}

.clearAllBtn{
    color: #e20303;
    display: block;
}
</style>