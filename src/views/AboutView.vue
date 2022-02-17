<template>
<div class="content">
    <h1 id="title" class="content--center">freeCodeCamp Survey Form</h1>
    <p id="description" class="content--center">
      Thank you for taking the time to help us improve the platform
    </p>
    <form  id="survey-form" class="content__form" @submit.prevent="submit()">
      <div class="row">
        <div class="col content__form__label">
          <label for="name" id="name-label">Name:</label>
        </div>
        <div class="col-md-12">
          <input
            type="text"
            class="form-control"
            id="name"
            name="name"
            placeholder="Enter your name"
            v-model="name"
          />
        </div>
        <div
          :class="{ active: isNameActive, 'text-danger': hasNameError }"
        >Name must be filled out</div>
      </div>

      <div class="row">
        <div class="col content__form__label">
          <label for="email" id="email-label">Email:</label>
        </div>
        <div class="col-md-12">
          <input
            type="email"
            class="form-control"
            id="email"
            name="email"
            placeholder="Enter your email"
            v-model="email"
          />
        </div>
        <div
          :class="{ active: isEmailActive, 'text-danger': hasEmailError }"
        >{{emailErrorMessage}}</div>
      </div>

      <div class="row">
        <div class="col content__form__label">
          <label for="age" id="number-label">Age:</label>
        </div>
        <div class="col-md-12">
          <input
            type="number"
            class="form-control"
            id="age"
            name="age"
            min="9"
            max="100"
            placeholder="Age"
            v-model="age"
          />
        </div>
      </div>

      <div class="row">
        <div class="col content__form__label">
          <label for="phone" id="phone-label">Phone:</label>
        </div>
        <div class="col-md-12">
          <input
            type="text"
            class="form-control"
            id="phone"
            name="phone"
            placeholder="Phone number"
            v-model="phone"
          />
        </div>
        <div
          :class="{ active: isPhoneActive, 'text-danger': hasPhoneError }"
        >{{phoneErrorMessage}}</div>
      </div>

      <div class="row">
        <div class="col content__form__label">
          <label for="role"
            >Which option best describes your current role?</label
          >
        </div>
        <div class="col-md-12">
          <select v-model="role" id="role" name="role" class="form-control">
            <option disabled selected value>Select current role</option>
            <option v-for="option in options" :value="option.value">
              {{ option.text }}
            </option>
          </select>
        </div>
      </div>

      <div class="row">
        <div class="col content__form__label">
          <label for="userRecommend"
            >Would you recommend freeCodeCamp to a friend?</label
          ><br />
        </div>
        <div class="col-md-12">
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="radio"
                class="form-check-input"
                value="definitely"
                name="userRecommend"
                v-model="userRecommend"
              />Definitely
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="radio"
                class="form-check-input"
                value="maybe"
                name="userRecommend"
                v-model="userRecommend"
              />Maybe
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="radio"
                class="form-check-input"
                value="not-sure"
                name="userRecommend"
                v-model="userRecommend"
              />Not sure
            </label>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col content__form__label">
          <label for="prefer"
            >What would you like to see improved? (Check all that apply)</label
          >
        </div>
        <div class="col-md-12">
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                value="front-end-projects"
                v-model="prefer"
              />Front-end Projects
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                value="back-end-projects"
                v-model="prefer"
              />Back-end Projects
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                value="data-visualization"
                v-model="prefer"
              />Data Visualization
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                value="challenges"
                v-model="prefer"
              />Challenges
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                value="open-source-community"
                v-model="prefer"
              />Open Source Community
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                value="gitter-help-rooms"
                v-model="prefer"
              />Gitter help rooms
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                value="videos"
                v-model="prefer"
              />Videos
            </label>
          </div>
          <div class="form-check-inline">
            <label class="form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                value="forum"
                v-model="prefer"
              />Forum
            </label>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col content__form__label">Any comments or suggestions?</div>
        <div class="col-md-12">
          <textarea
            class="form-control"
            rows="6"
            cols="5"
            id="comment"
            v-model="comment"
          ></textarea>
        </div>
      </div>
    <div class="row">
      <div class="col content__form__button">
        <button class="btn btn-success" id="submit" type="submit">
          Submit
        </button>
      </div>
    </div>
    </form>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      name: "",
      email: "",
      age: 9,
      phone: "",
      role: "",
      userRecommend: "maybe",
      prefer: [],
      comment: "",
      options: [
        { text: "Student", value: "student" },
        { text: "Full Time Job", value: "full-time-job" },
        { text: "Full Time Learner", value: "full-time-learner" },
        { text: "Prefer not to say", value: "prefer-not-to-say" },
        { text: "Other", value: "other" },
      ],
      mailformat:  /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/,
      vnf_regex: /((09|03|07|08|05)+([0-9]{8})\b)/g,
      hasNameError: false,
      isNameActive: true,
      hasEmailError: false,
      isEmailActive: true,
      hasPhoneError: false,
      isPhoneActive: true,
      nameErrorMessage:"",
      emailErrorMessage:"",
      phoneErrorMessage:"",
    };
  },
  created() {
    console.log(`the component is now created`);
  },
  mounted() {
    console.log(`the component is now mounted.`);
  },
  watch: {
     name(value){
      this.name = value;
       if (this.name == "") {
        this.hasNameError = true;
        this.isNameActive = false;
        this.nameErrorMessage = "Name must be filled out";
      }
      else {
        this.hasNameError = false;
        this.isNameActive = true;
      } 
    },

     email(value){
      this.email = value;
      if (this.email != "") {
        this.hasEmailError = false;
        this.isEmailActive = true;
         if (!this.email.match(this.mailformat)) {
          this.hasEmailError = true;
          this.isEmailActive = false;
          this.emailErrorMessage = "You have entered an invalid email address!";
        }
      } else {
          this.hasEmailError = true;
          this.isEmailActive = false;
          this.emailErrorMessage = "Email must be filled out!";
      }
    },

     phone(value){
      this.phone = value;
      if (this.phone !== "") {
          this.hasPhoneError = false;
          this.isPhoneActive = true;
          if (this.vnf_regex.test(this.phone) == false) {
            this.hasPhoneError = true;
            this.isPhoneActive = false;
            this.phoneErrorMessage = "Invalid phone number!";
          }
      } else {
          this.hasPhoneError = true;
          this.isPhoneActive = false;
          this.phoneErrorMessage = "Phone must be filled out!";
      }
    }
  },
  computed: {},
  methods: {
    submit() {
      if(this.name == ""){
        alert("Name must be filled out!");
      }
      if(this.email == ""){
        alert("Email must be filled out!");
      }
      if(this.phone == ""){
        alert("Phone must be filled out!");
      }
      console.log(
        this.name,
        this.email,
        this.age,
        this.phone,
        this.role,
        this.userRecommend,
        this.comment
      );
      this.prefer.forEach((element) => {
        console.log(element);
      });
    },
  },
};
</script>
<style>
body {
  background-color: rgb(254, 236, 225);
}
.active{
  display: none;
}
.content {
  margin-top: 120px;
  font-family: Tahoma, Verdana, sans-serif;
}

.content--center {
  text-align: center;
}

.content__form {
  width: 800px;
  margin: 0px auto;
  background-color: white;
  border-radius: 2%;
  padding: 30px;
}

.content__form__label {
  padding-top: 10px;
}

.content__form__button {
  text-align: center;
  padding-top: 10px;
}
</style>
