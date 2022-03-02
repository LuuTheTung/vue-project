<template>
  <div class="row" style="padding-top: 1rem">
    <div class="col-md-10">
      <input
        class="form-control"
        type="text"
        placeholder="Type a job"
        v-model="title"
      />
    </div>
    <div class="col-md-2">
      <button class="btn btn-primary" @click="addItem">Add</button>
    </div>
  </div>
</template>

<script lang="ts">
import { reactive, ref } from "vue";
import { uuid } from "vue-uuid";
export default {
  name: "AddItem",
  props: [""],
  setup(props, context) {
    const title = ref("");

    const addItem = () => {
      const item = reactive({
        title: title.value,
        completed: false,
        userId: 1,
        id: uuid.v4(),
      });
      context.emit("add-item", item);
    };
    return {
      title,
      addItem,
    };
  },
};
</script>

<style></style>
