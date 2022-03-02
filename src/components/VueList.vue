<template>
  <div class="content">
    <div class="content__form center">
      <table class="table table-hover table-bordered caption-top">
        <caption>
          List of users
        </caption>
        <thead>
          <th scope="col" v-for="(head, index) in listTableHead" :key="index">
            {{ head }}
          </th>
        </thead>
        <tbody>
          <tr v-for="(user, index) in listUser" :key="index">
            <td>{{ user.id }}</td>
            <td style="cursor: pointer">
              {{ user.name }}
            </td>
            <td>{{ user.email }}</td>
            <td>{{ user.phone }}</td>
            <td>{{ user.address.street }} - {{ user.address.city }}</td>
            <td>
              <button
                class="btn btn-success"
                data-bs-toggle="modal"
                data-bs-target="#exampleModal"
                @click="mapUserData(user.id)"
              >
                Edit
              </button>
            </td>
            <td>
              <button class="btn btn-danger" @click="deleteItem(user.id)">
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- Modal -->
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Edit user</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <NameField v-model="user.name" :nameProp="user.name"
              >Name:</NameField
            >
            <EmailField v-model="user.email" :emailProp="user.email"
              >Email:</EmailField
            >
            <PhoneField v-model="user.phone" :phoneProp="user.phone" 
              >Phone number:</PhoneField
            >
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <button type="button" class="btn btn-primary" @click="saveChange">
              Save changes
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import axios from "axios";
import { reactive, ref } from "vue";
import NameField from "./NameField.vue";
import EmailField from "./EmailField.vue";
import PhoneField from "./PhoneField.vue";
// import VueItem from "./VueItem.vue";
export default {
  name: "VueList",
  components: { NameField, EmailField, PhoneField },
  setup(props) {
    const listTableHead = ref([
      "Id",
      "Name",
      "Email",
      "Phone",
      "Address",
      "Edit",
      "Delete",
    ]);
    const listUser = ref([]);

    const userId = ref("");
    const user = reactive({
      name: "",
      email: "",
      phone: "",
    });
    const address = ref("");
    const getListUser = async () => {
      try {
        const res = await axios.get(
          `https://jsonplaceholder.typicode.com/users`
        );
        listUser.value = res.data;
      } catch (error) {
        console.log(error);
      }
    };
    getListUser();

    const mapUserData = (id) => {
      const userData = ref([]);
      userData.value = listUser.value.filter(item => item.id == id);
      console.log(userData.value)
      user.name = userData.value[0].name;
      user.email = userData.value[0].email;
      user.phone = userData.value[0].phone;
      userId.value = id;
    };

    const saveChange = async () => {
      try {
        await axios.put(
          `https://jsonplaceholder.typicode.com/users/${userId.value}`,
          user
        );
      } catch (error) {
        console.log(error);
      }
      listUser.value.forEach(item => {
        if(item.id == userId.value){
          item.name = user.name;
          item.email = user.email;
          item.phone = user.phone
        }
      })
    };

    const deleteItem = async (id) => {
      try {
        console.log(id);
        await axios.delete(`https://jsonplaceholder.typicode.com/users/${id}`);
        listUser.value = listUser.value.filter((item) => item.id !== id);
      } catch (error) {
        console.log(error);
      }
    };

    return {
      listUser,
      listTableHead,
      user,
      address,
      getListUser,
      saveChange,
      deleteItem,
      mapUserData,
      
    };
  },
};
</script>

<style></style>
