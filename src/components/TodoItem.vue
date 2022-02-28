<template>
  <div>
    <div class="row" style="padding-top: 1rem">
      <div class="col-md-10">
        <div class="form-check">
          <input
            type="checkbox"
            class="form-check-input"
            :checked="todoProps.completed"
            v-on:change="changeStatus"
            :id="todoProps.id"
          />
          <label
            class="form-check-label"
            :class="[todoProps.completed == true ? 'text-deco' : '']"
            :for="todoProps.id"
          >
            {{ todoProps.title }}
          </label>
        </div>
      </div>
      <div class="col-md-2">
        <button class="btn btn-warning" @click="deleteItem">Delete</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref } from "vue";
export default {
  name: "TodoItem",
  props: ["todoProps"],
  setup(props, context) {
    const changeStatus = () => {
      context.emit("change-completed", props.todoProps.id);
    };
    const deleteItem = () => {
      context.emit("delete-item", props.todoProps.id);
    };
    return {
      changeStatus,
      deleteItem,
    };
  },
};
</script>

<style>
</style>