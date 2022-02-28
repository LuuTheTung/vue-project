<template>
  <div class="content">
    <div class="content__center">
      <h2>Todo List with props and event</h2>
      <AddItem @add-item="addItemToList" />
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todoProps="todo"
        @change-completed="markComplete"
        @delete-item="deleteItem"
      />
    </div>
  </div>
</template>
<script lang="ts">
import TodoItem from "@/components/TodoItem.vue";
import AddItem from "@/components/AddItem.vue";
import { ref } from "vue";
import axios from "axios";
export default {
  name: "Todo",
  components: { TodoItem, AddItem },
  setup(props) {
    // todo list
    const todos = ref([]);
    
    const getTodos = async () => {
      try {
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/todos?_limit=10"
        );
        todos.value = res.data;
      } catch (error) {
        console.log(error);
      }
    };
    getTodos();
    const markComplete = (id) => {
      todos.value.forEach((item) => {
        item.id == id ? (item.completed = !item.completed) : item.completed;
      });
    };
    const deleteItem = async (id) => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        todos.value = todos.value.filter((item) => item.id !== id);
      } catch (error) {
        console.log(error);
      }
    };

    const addItemToList = async (item) => {
        console.log(item);
        try {
            await axios.post(`https://jsonplaceholder.typicode.com/todos/`, item);
            todos.value.push(item);
        } catch (error) {
            console.log(error);
        }
    }
    return {
      todos,
      markComplete,
      deleteItem,
      getTodos,
      addItemToList
    };
  },
};
</script>

<style>
.content {
  margin-top: 120px;
  font-family: Tahoma, Verdana, sans-serif;
}
.text-deco {
  text-decoration: line-through;
}
.content__center {
  width: 800px;
  margin: 0px auto;
  background-color: white;
  border-radius: 2%;
  padding: 30px;
}
</style>