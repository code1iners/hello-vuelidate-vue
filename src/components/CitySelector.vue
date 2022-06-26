<template>
  <div class="input__wrapper">
    <div class="input-selector__container">
      <select class="input-selector" v-model="city">
        <option disabled value="">Please select one</option>
        <option>Seoul</option>
        <option>Busan</option>
        <option>Daegu</option>
      </select>
    </div>

    <span class="input-error" v-for="error in errors" :key="error.$uid">
      {{ error.$message }}
    </span>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import { ErrorObject } from "@vuelidate/core";

interface CitySelectorProps {
  modelValue: string;
  errors?: ErrorObject[];
}

export default defineComponent({
  name: "CitySelector",
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
  setup(props: CitySelectorProps, { emit }) {
    const city = computed({
      get: () => props.modelValue,
      set: (val) => emit("update:modelValue", val),
    });

    return {
      city,
    };
  },
});
</script>

<style scoped>
.form__container .input-selector {
  width: 100%;
  padding: 10px;
}
</style>
