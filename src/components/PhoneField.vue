<template>
  <div class="row" style="padding-top: 10px">
    <div class="col-md-4"><slot></slot></div>
    <div class="col-md-8">
      <input
        type="text"
        class="form-control"
        v-model="phone"
        @input="$emit('update:modelValue', $event.target.value)"
      />
    <div :class="{'text-danger': hasPhoneError }">
      {{ phoneErrorMessage }}
    </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref, toRef, watch } from "vue";
export default {
  name: "PhoneField",
  props: ["phoneProp"],
  setup(props, context) {
    let phone = ref("");
    let phoneProp = toRef(props, "phoneProp");
    // props are used to pass reactive data from parent components to child components.
    //  The pattern is: events from child to parent, mutation from parent to child .
    //  toRef makes the data reactive, but it doesn't affect whether you can mutate it.

    let hasPhoneError = ref(false);
    let phoneErrorMessage = ref("");
    watch(phoneProp, (value) => {
      phone.value = phoneProp.value;
      if (phone.value == "") {
        hasPhoneError.value = true;
        phoneErrorMessage.value = "Phone must be filled out!";
      } else {
        hasPhoneError.value = false;
        phoneErrorMessage.value = "";
      }
    });

    return {
      phone,
      hasPhoneError,
      phoneErrorMessage,
    };
  },
};
</script>

<style></style>
