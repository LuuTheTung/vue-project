<template>
  <div class="row" style="padding-top: 10px">
    <div class="col-md-4"><slot></slot></div>

    <div class="col-md-8">
      <input
        type="text"
        class="form-control"
        :value="nameProp"
        @input="$emit('update:modelValue', $event.target.value)"
      />
    <div :class="{ 'text-danger': hasNameError }">
      {{ nameErrorMessage }}
    </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref, toRef, watch } from "vue";
export default {
  name: "NameField",
  components: {},
  props: ["nameProp"],

  setup(props, context) {
    let hasNameError = ref(false);
    let nameErrorMessage = ref("");
    let name = ref("");
    let nameProp = toRef(props, "nameProp");
    watch(nameProp, (value) => {
      name.value = nameProp.value;
      if (name.value == "") {
        hasNameError.value = true;
        nameErrorMessage.value = "Name must be filled out!";
      } else {
        hasNameError.value = false;
        nameErrorMessage.value = "";
      }
    });
    return {
      hasNameError,
      nameErrorMessage,
      name,
    };
  },
};
</script>

<style></style>
