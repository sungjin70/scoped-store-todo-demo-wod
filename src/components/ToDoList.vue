<template>

    <v-card class="elevation-12">
        <v-toolbar dark :color="done ? 'blue lighten-1' : 'gray lighten-2'">
            <v-toolbar-title>Todos Done</v-toolbar-title>
        </v-toolbar>
        <v-card-text>
        <ul>
            <li v-for="(todo, i) in todoList"
                :key="i"
                :class="{ active: selectedTodoId === todo.id }"
                class="transition-swing text-subtitle-1"
                @click="selectedTodoId = todo.id">
                {{ todo.title }} 
                <v-spacer></v-spacer>
                <v-chip
                    v-if="todo.isBusiness"
                    class="ma-2 text-subtitle-3"
                    color="green"
                    text-color="white"
                    >
                    Business
                </v-chip>
                <v-chip
                    v-if="todo.isPrivate"
                    class="ma-2 text-subtitle-3"
                    color="secondary"
                    text-color="white"
                    >
                    Private
                </v-chip>
            </li>
        </ul>
        </v-card-text>
    </v-card>

</template>

<script>
import {filterTodos} from '@/utils/common-functions';

/**
 * ToDo 목록 출력 컴포넌트
 * 
 * A component that display the to-do list
*/
export default {
  name: 'ToDoList',
  data: () => ({
    todos:[],
    selectedTodoId:-1,
    filter:{},
  }),
  computed:{
      todoList:function() {
        const showDone = this.done;
        let todos = filterTodos(this.todos, this.filter).filter(t => t.isDone === showDone);
        return todos;
      }
  },
  props:['done'],
  globalStore:{
    selectedTodoId:{},
    todos:{},
    filter:{},
  }
}

</script>

<style scoped>
ul {
    list-style: none;
    margin: 0px;
    padding: 0px;
    width: 100%;
}

li {
    display: flex;
    flex-direction: row;
    align-items: center;
    height: 40px;
    padding-left: 8px;
    cursor: pointer;
}

li.active {
    background-color: rgb(226, 226, 236);
}
</style>