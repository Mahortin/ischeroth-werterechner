<script setup>
// import { ref, reactive, computed } from 'vue'
import { ref, reactive } from "vue";
// const count = ref(0);
const user = reactive({
  email: "",
  password: "",
});

const obj = ref({
  nested: { count: 0 },
  arr: ["foo", "bar"],
});

// eslint-disable-next-line
// function increment() {
//   count.value++;
// }

function login() {
  user.email = "john doe";
}

function mutateDeeply() {
  // these will work as expected.
  obj.value.nested.count++;
  obj.value.arr.push("baz");
}

const attributes = reactive([
  { key: "MU", name: "Mut", value: 8, increased: false },
  { key: "KL", name: "Klugheit", value: 8, increased: false },
  { key: "IN", name: "Intuition", value: 8, increased: false },
  { key: "CH", name: "Charisma", value: 8, increased: false },
  { key: "FF", name: "Fingerfertigkeit", value: 8, increased: false },
  { key: "GE", name: "Gewandheit", value: 8, increased: false },
  { key: "KO", name: "Konstitution", value: 8, increased: false },
  { key: "KK", name: "Körperkraft", value: 8, increased: false },
]);
</script>

<template>
  <div class="column">
    <h1>Eigenschaften</h1>
    <!-- count for ref example -->
    <!-- <button @click="increment">
      {{ count }}
    </button> -->

    <!-- count for reactive example -->
    <button @click="login">Login</button>
    <span> User logged in: {{ user.email }} </span>

    <button v-if="user.email == 'john doe'" @click="mutateDeeply">
      {{ obj.arr }}
      <!-- mybutton -->
    </button>

    <button @click="mutateDeeply">
      {{ obj.nested.count }}
      <!-- mybutton -->
    </button>

    <h1 Attributes></h1>
    <div
      v-for="attribute in attributes"
      :key="attribute.key"
      class="attribute-item"
    >
      <!-- <span> -->
      {{ attribute.name }}
      <div class="attribute-info">
        <span class="attribute-key">{{ attribute.key }}</span>
        <span class="attribute-name">{{ attribute.name }}</span>
      </div>
      <input
          type="number"
          min="8"
          max="16"
          @change="setAttribute(attribute)"
          v-model.number="attribute.value"
          :class="[attribute.increased ? 'attribute-input-highlighted' : 'attribute-input']"
        />
        <button
          :class="[attribute.increased ? 'highlight-button' : '']"
          @click="increaseAttribute(attribute)"
        >
          +
        </button>
        
    </div>

    <!-- <div v-for="attribute in attributes" :key="attribute.key" class="attribute-item">
        <div class="attribute-info">
          <span class="attribute-key">{{ attribute.key }}</span>
          <span class="attribute-name">{{ attribute.name }}</span>
        </div>
        <input
          type="number"
          min="8"
          max="16"
          @change="setAttribute(attribute)"
          v-model.number="attribute.value"
          :class="[attribute.increased ? 'attribute-input-highlighted' : 'attribute-input']"
        />
        <button
          :class="[attribute.increased ? 'highlight-button' : '']"
          @click="increaseAttribute(attribute)"
        >
          +
        </button>
      </div> -->
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

button {
  padding: 10px 20px;
  margin: 10px;
  border: none;
  border-radius: 8px; /* Softer edges with rounded corners */
  background-color: #f8f2e8; /* Light gray background */
  color: #333; /* Darker font color */
  font-size: 16px;
  cursor: pointer;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* Soft shadow for depth */
  transition:
    background-color 0.3s ease,
    box-shadow 0.3s ease; /* Smooth transition effects */
}

/* Active state: Change only the background color */
button.highlight-button {
  background-color: #3acf4b; /* Modern blue background for active state */
  color: #713604; /* Change the font color to white when active */
}

/* Hover state: Slight background change and shadow lift */
button:hover {
  background-color: #f5ebda; /* Light gray on hover for normal buttons */
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15); /* Increase shadow for hover effect */
}

/* Hover state for active button */
button.highlight-button:hover {
  background-color: #51cf5f; /* Slightly darker blue on hover */
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15); /* Increase shadow for hover effect */
}

.container {
  display: flex;
  justify-content: space-between;
}
.attribute-item,
.skill-item {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  white-space: nowrap; /* Prevent line breaks within the items */
}

.attribute-input {
  flex-shrink: 0;
}

.attribute-input-highlighted {
  flex-shrink: 0;
  color: #3acf4b;
}

button.highlight-button {
  background-color: #3acf4b; /* Modern blue background for active state */
  color: #713604; /* Change the font color to white when active */
}

.column {
  width: 48%;
}
</style>
