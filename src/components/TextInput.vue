<template>
  <div class="input__wrapper">
    <input
      class="input-text"
      :type="type"
      :placeholder="placeholder"
      v-model="inputText"
    />
    <span class="input-error" v-for="error in errors" :key="error.$uid">
      {{ error.$message }}
    </span>
  </div>
</template>

<script lang="ts">
import { ErrorObject } from "@vuelidate/core";
import { computed, defineComponent, PropType } from "vue";

interface TextInputProps {
  modelValue: string;
  placeholder?: string;
  errors?: ErrorObject[];
}

export default defineComponent({
  name: "TextInput",
  props: {
    modelValue: {
      type: String,
      required: true,
    },
    errors: {
      type: Array as PropType<ErrorObject[]>,
      required: false,
    },
    placeholder: {
      type: String,
      default: () => "Enter input",
    },
    type: {
      type: String,
      default: () => "text",
    },
  },
  emits: ["update:modelValue"],
  setup(props: TextInputProps, { emit }) {
    const inputText = computed({
      get: () => props.modelValue,
      set: (val) => emit("update:modelValue", val),
    });

    return {
      inputText,
    };
  },
});
</script>

<style scoped>
.input-text {
  padding: 10px;
}
</style>
