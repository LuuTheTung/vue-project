<template>
  <div class="row" style="padding-top: 10px">
    <div class="col-md-4"><slot></slot></div>
    <div class="col-md-8">
      <input
        type="email"
        class="form-control"
        :value="emailProp"
        @input="$emit('update:modelValue', $event.target.value)"
      />
      <div :class="{ 'text-danger': hasEmailError }">
        {{ emailErrorMessage }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref, toRef, watch } from "vue";
export default {
  name: "EmailField",
  props: ["emailProp"],
  setup(props) {
    let email = ref("");
    let emailProp = toRef(props, "emailProp");
    let mailformat = ref("/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/");
    // let isEmailActive = ref(true);
    let hasEmailError = ref(false);
    let emailErrorMessage = ref("");
    watch(emailProp, (value) => {
      email.value = emailProp.value;
      if (email.value == "") {
        hasEmailError.value = true;
        emailErrorMessage.value = "Email must be filled out!";
      } else {
        if (!email.value.match(mailformat.value)) {
          console.log(!email.value.match(mailformat.value))
          // console.log(email.value, mailformat.value)
          hasEmailError.value = true;
          emailErrorMessage.value =
            "";
        } else {
          hasEmailError.value = false;
          emailErrorMessage.value = "You have entered an invalid email address!";
        }
      }
    });
    return {
      email,
      mailformat,
      hasEmailError,
      emailErrorMessage,
    };
  },
};
</script>

<style></style>
