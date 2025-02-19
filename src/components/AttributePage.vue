<script setup>
// import { ref, reactive, computed } from 'vue'
import { ref, reactive } from "vue";
import SingleAttribute from "./SingleAttribute.vue";
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

function setAttribute(attribute) {
  attribute.increased = false;
}

function increaseAttribute(attribute) {
  attribute.increased = !attribute.increased;
  attribute.value = attribute.increased
    ? attribute.value + 1
    : attribute.value - 1;
  // calcEverythingAssociated(attribute.key)
}

function warning() {
  window.confirm("sometext");
}
</script>

<template>
  <div class="column">
    <h1>Eigenschaften</h1>
    <SingleAttribute
      v-for="attribute in attributes"
      :key="attribute.key"
      :attributeKey="attribute.key"
      :attributeName="attribute.name"
      :attributeValue="attribute.value"
      @attribute-changed="warning()"
    >
    </SingleAttribute>
    <button @click="warning">WARNING!</button>
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
        :class="[
          attribute.increased
            ? 'attribute-input-highlighted'
            : 'attribute-input',
        ]"
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
@import "../assets/shared-styles.scss";
</style>
