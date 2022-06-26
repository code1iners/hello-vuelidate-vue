<template>
  <div class="input__wrapper">
    <div class="input-gender__container">
      <div class="input-gender__wrapper">
        <label for="input-gender-male">MALE</label>
        <input
          id="input-gender-male"
          type="radio"
          value="MALE"
          v-model="gender"
        />
      </div>

      <div class="input-gender__wrapper">
        <label for="input-gender-female">FEMALE</label>
        <input
          id="input-gender-female"
          type="radio"
          value="FEMALE"
          v-model="gender"
        />
      </div>
    </div>

    <span class="input-error" v-for="error in errors" :key="error.$uid">
      {{ error.$message }}
    </span>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import { ErrorObject } from "@vuelidate/core";

interface GenderInputProps {
  modelValue: string;
  errors?: ErrorObject[];
}

export default defineComponent({
  name: "GenderInput",
  props: {
    modelValue: {
      type: String,
      required: true,
    },
    errors: {
      type: Array as PropType<ErrorObject[]>,
      required: false,
    },
  },
  emits: ["update:modelValue"],
  setup(props: GenderInputProps, { emit }) {
    const gender = computed({
      get: () => props.modelValue,
      set: (val) => emit("update:modelValue", val),
    });

    return {
      gender,
    };
  },
});
</script>

<style scoped>
.form__container .input-gender__container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.form__container .input-gender__wrapper {
  display: flex;
  align-items: center;
  gap: 5px;
}
</style>
