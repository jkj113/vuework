<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in todoItems" v-bind:key="index" class="shadow">
               <!-- <i class="fas fa-check checkBtn" @click="toggleComplete"></i>
                {{todoItem.item}} -->
                <i class="fas fa-check checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" @click="toggleComplete(todoItem, index)"></i>
                <span v-bind:class="{textCompleted: todoItem.completed }">{{todoItem.item}}</span>
                <span class="removeBtn" @click="removeTodo(todoItem, index)">
                   <i class="fas fa-trash-alt"></i> 
                </span> 
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            todoItems: []
        }
    },
    methods: {
        toggleComplete: function(todoItem) {
            todoItem.completed = !todoItem.completed;
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        },
        
        removeTodo: function(todoItem, index) {
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
        }
    },
    /* life cycle method */
    created: function() {
        if(localStorage.length > 0){
            for(var i = 0; i < localStorage.length; i++){
                // this.todoItems.push(localStorage.key(i));
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    var itemJson = localStorage.getItem(localStorage.key(i));
                    this.todoItems.push(JSON.parse(itemJson));
                }
            }
        }
    }
}
</script>

<style scoped>
ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left; 
}

li {
    display: flex;
    min-height: 50px;
    height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}

.removeBtn{
    margin-left: auto;
    color: #de4343;
}

.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}

.checkBtnCompleted {
    color: #b3adad;
}

.textCompleted {
    text-decoration: line-through;
    color: #b3adad;
}
</style>