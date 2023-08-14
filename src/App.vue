<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Hello my name is Fabien welcome on my App..."/> -->

  <div v-text="greet"></div>
  <div>{{ firstName }} - {{ lastName }}</div>
  <div v-html="country"></div>
  <h1 v-bind:id="heading">Heading</h1>
  <!-- <button v-bind:disabled="isDisabled">Submit</button> -->
  <h2 class="underline">Text decoration</h2>
  <h2 v-bind:class="position && 'title'">Sofware Developer</h2>
  <p v-bind:class="workStatus ? 'working' : 'notworking'">working</p>
  <p v-bind:class="['underline', 'working']">Tools : Laravel, Vue.js</p>

  <!-- Binding style -->

  <p
    v-bind:style="{
      color: highlight,
      'font-size': textSize + 'px',
      'font-weight': boldText,
    }"
  >
    Don't hate the player hate the game...
  </p>

  <p v-bind:style="styleObject">Style using Object</p>

  <p v-bind:style="[baseStyle, moreStyle]">Style using Array</p>

  <!-- Conditionnal structure -->
  <h2 v-bind:class="['underline', 'working']">Condition in vue</h2>
  <p v-if="num === 0">num is equal to 0</p>
  <p v-else-if="num < 0">num is a negative number</p>
  <p v-else>num is a positive number</p>

  <div v-if="showInfos == true" v-bind:style="moreStyle">
    <h2>Fabien</h2>
    <h2>Louce Kerdely</h2>
    <h2>Software Developer</h2>
  </div>

  <p v-if="isActive == true">Active</p>
  <p v-show="isActive == true">Active</p>

  <!-- for loop with view -->

  <h2 v-bind:class="'notworking'">For loop with view</h2>
  <h3 v-for="info in personalInfos" :key="info">{{ info }}</h3>
  <hr />
  <h3 v-for="moreInfo in moreInfos" :key="moreInfo">
    {{ moreInfo.fname }} {{ moreInfo.lname }} {{ moreInfo.age }} ans.
  </h3>
  <hr />
  <div v-for="other in otheInfos" :key="other" v-bind:class="'title'">
    <h2>{{ other.name }}</h2>
    <h4 v-for="(movie, index) in other.movies" :key="movie">
      {{ index }} {{ movie }}
    </h4>
    ---
  </div>

  <!-- methods -->
  <hr />
  <h2>methods</h2>
  <h4>Methods result: {{ add(10, 20, 30) }}</h4>

  <!-- events -->
  <hr />
  <h2>Events</h2>
  <h2>{{ incr }}</h2>
  <button v-on:click="incr += 1">Increment +1</button>
  <button v-on:click="incr -= 1">Decrement -1</button>

  <button v-on:click="incrementValue(100)">Increment</button>
  <button @click="decrementValue(100)">Decrement</button>

  <button @click="resetValue(0)">Reset</button>

  <hr />
  <h2>Form Handlers</h2>

  <form v-on:submit.prevent="submitForm">
    <p>{{ JSON.stringify(formData) }}</p>
    <div>
      <label for="name">Name : </label>
      <input type="text" id="name" v-model.trim="formData.name" />
    </div>
    <br />
    <div>
      <label for="profile"> Profile summary : </label>
      <textarea id="profile" v-model="formData.profile"></textarea>
    </div>
    <br />
    <div>
      <label for="country">Country : </label>
      <select id="country" v-model="formData.country">
        <option value="">Select a country</option>
        <option value="vietnam">Vietnam</option>
        <option value="singapore">Singapore</option>
        <option value="thailand">Thailand</option>
      </select>
    </div>

    <br />
    <div>
      <label for="location">Job location : </label>
      <select id="location" multiple v-model="formData.location">
        <option value="vietnam">Vietnam</option>
        <option value="singapore">Singapore</option>
        <option value="thailand">Thailand</option>
      </select>
    </div>
    <br />

    <div>
      <label for="remote">Remote : </label>
      <input type="checkbox" id="remote" v-model="formData.remote" />
    </div>

    <br />
    <div>
      <label>Skills : </label>
      <label for="html">Html</label>
      <input type="checkbox" value="html" id="html" v-model="formData.skills"/>

      <label for="php">PHP</label>
      <input type="checkbox" id="php" value="php" v-model="formData.skills" />

      <label for="js">JavaScript</label>
      <input type="checkbox" id="js" value="js" v-model="formData.skills" />
    </div>

    <br>
    <div>
      <label>Year of experience : </label>
      <label for="0-2">0-2 years: </label>
      <input type="radio" value="0-2" id="0-2" v-model="formData.yearOfExperience"/>

      <label for="3-5">3-5 years: </label>
      <input type="radio" id="3-5" value="3-5" v-model="formData.yearOfExperience" />

      <label for="6-10">6-10 years: </label>
      <input type="radio" id="6-10" value="6-10" v-model="formData.yearOfExperience" />

      <label for="10+">10+ years: </label>
      <input type="radio" id="10+" value="10+" v-model="formData.yearOfExperience" />
    </div>

    <div>
      <input @keyup.enter="submitForm" type="submit" value="submit">
    </div>
  </form>
<hr>
<h2>Computed</h2>
<h2>Method total : {{ methodArrayTotal() }}</h2>
<h2>Computed total : {{ getTotal }}</h2>
<!-- <button v-on:click="computeArray.push(50)">Add 50</button> -->

<!-- Watchers -->

</template>
<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  // components: {
  //   HelloWorld
  // }
  data() {
    return {
      greet: "Good morning",
      firstName: "Louce Kerdely",
      lastName: "Fabien",
      country: "<b>Vietnam</b>",
      heading: "Heading",
      position: true,
      workStatus: true,
      isDisabled: false,
      highlight: "orange",
      textSize: 30,
      boldText: "bold",

      styleObject: {
        fontSize: "30px",
        fontWeight: "bold",
        color: "purple",
      },

      baseStyle: {
        fontSize: "30px",
        fontWeight: "bold",
      },
      moreStyle: {
        color: "blue",
        backgroundColor: "#DDDDDD",
        padding: "10px",
      },
      num: 0,
      showInfos: true,
      isActive: false,

      personalInfos: [
        "Fabien",
        "Louce Kerdely",
        28,
        "Vietnam",
        "Hanoi",
        "Software Developer",
      ],
      moreInfos: [
        { fname: "Fab", lname: "Doe", age: 28 },
        { fname: "Loosker", lname: "Kerd", age: 25 },
        { fname: "Loos", lname: "Fab", age: 23 },
      ],

      otheInfos: [
        {
          name: "Ben affleck",
          movies: ["Batman", "The accountant", "Triple Frontier"],
        },
        {
          name: "Leonardo Dicaprio",
          movies: ["Titanic", "The revenant", "Don't look up"],
        },
        {
          name: "Jason startham",
          movies: ["The transporter", "Parker", "Wrath of man"],
        },
      ],

      incr: 0,

      formData: {
        name: "",
        profile: "",
        country: "",
        location: [],
        remote: false,
        skills: [],
        yearOfExperience: ''
      },

    computeArray: [10, 20, 30, 40, 50],

    };
  },
  methods: {
    add(vOne, vTwo, vThree) {
      return vOne + vTwo + vThree;
    },

    incrementValue(i) {
      return (this.incr += i);
    },
    decrementValue(d) {
      return (this.incr -= d);
    },
    resetValue(r) {
      return (this.incr = r);
    },

    submitForm(){
      console.log('Data: ', this.formData)
    },
    methodArrayTotal(){
      console.log("Method property")
      return this.computeArray.reduce((a, b)=> ( a + b), 0)
    }
  },

  computed:{
    getTotal(){
        console.log("Computed property")
        return this.computeArray.reduce((a, b)=> ( a + b), 0)
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.underline {
  text-decoration: underline;
}
.title {
  color: cornflowerblue;
}
.working {
  color: green;
}
.notworking {
  color: red;
}
</style>
