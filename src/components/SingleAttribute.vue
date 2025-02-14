<script setup>
// import { ref, reactive, computed } from 'vue'
// import { ref, reactive } from "vue";
import { defineProps, defineEmits } from "vue";

defineProps({
  attributeKey: String,
  attributeName: String,
  attributeValue: Number,
});

const emit = defineEmits(['attribute-changed'])

function attributeChanged(){
  emit
}
</script>

<template>
  <!-- <h4>{{ attributeName }}</h4>
  <h5>{{ attributeKey }}</h5>
  <h5>{{ attributeValue }}</h5> -->

  <div class="attribute-info">
    <span class="attribute-key">{{ attributeKey }}</span>
    <span class="attribute-name">{{ attributeName }}</span>
  </div>
  <input
    type="number"
    value="{{ attributeValue }}"
    min="8"
    max="16"
    @change="attributeChanged(attribute)"
  />
  <!-- <input
          type="number"
          min="8"
          max="16"
          @change="setAttribute(attribute)"
          v-model.number="attribute.value"
          :class="[attribute.increased ? 'attribute-input-highlighted' : 'attribute-input']"
        /> -->
  <!-- <button
          :class="[attribute.increased ? 'highlight-button' : '']"
          @click="increaseAttribute(attribute)"
        >
          +
        </button> -->
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped> @import 'shared-styles.scss'</style>
