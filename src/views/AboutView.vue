<template>
<div style="display: flex">

  <div>Checked names: {{ checkedNames }}</div>

  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>

  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>

  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>
</div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      checkedNames: [],
    };
  },
  computed: {},
};
</script>
<style>
.greeting {
  color: red;
  font-weight: bold;
}
</style>
