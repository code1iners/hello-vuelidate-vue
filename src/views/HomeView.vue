<template>
  <div id="home__container">
    <form class="form__container" @submit.prevent="onSubmitClick">
      <TextInput
        v-model="state.userId"
        placeholder="Enter user id"
        type="text"
        :errors="v$.userId.$errors"
      />

      <TextInput
        v-model="state.username"
        type="text"
        placeholder="Enter username"
        :errors="v$.username.$errors"
      />

      <TextInput
        v-model="state.password"
        type="password"
        placeholder="Enter password"
        :errors="v$.password.$errors"
      />

      <TextInput
        v-model="state.confirmPassword"
        type="password"
        placeholder="Enter confirm password"
        :errors="v$.confirmPassword.$errors"
      />

      <GenderInput v-model="state.gender" :errors="v$.gender.$errors" />

      <CitySelector v-model="state.city" :errors="v$.city.$errors" />

      <button type="submit">submit</button>
    </form>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, reactive } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { minLength, required, sameAs, helpers } from "@vuelidate/validators";
import TextInput from "@/components/TextInput.vue";
import GenderInput from "@/components/GenderInput.vue";
import CitySelector from "@/components/CitySelector.vue";

interface SignUpForm {
  userId: string;
  username: string;
  password: string;
  confirmPassword: string;
  gender: string;
  city: string;
}

export default defineComponent({
  name: "HomeView",
  components: { TextInput, GenderInput, CitySelector },
  setup() {
    const state = reactive<SignUpForm>({
      userId: "",
      username: "",
      password: "",
      confirmPassword: "",
      gender: "MALE",
      city: "",
    });

    const userIdContainsA = (userId: string) => {
      return userId.toLowerCase().includes("a");
    };

    const rules = computed(() => ({
      userId: {
        required: helpers.withMessage("User id is required", required),
        minLength: helpers.withMessage(
          "User id should be at least 8 characters long.",
          minLength(8)
        ),
        userIdContainsA: helpers.withMessage(
          "The user id should be contains a char.",
          userIdContainsA
        ),
      },
      username: {
        required: helpers.withMessage("Username is required.", required),
      },
      password: {
        required: helpers.withMessage("Password is required.", required),
      },
      confirmPassword: {
        required: helpers.withMessage(
          "Confirm password is required.",
          required
        ),
        sameAs: helpers.withMessage(
          "The confirm password must be equal to the password.",
          sameAs(state.password)
        ),
      },
      gender: {
        required: helpers.withMessage("Gender is required.", required),
      },
      city: { required: helpers.withMessage("City is required.", required) },
    }));

    const v$ = useVuelidate<SignUpForm>(rules, state);

    const onSubmitClick = async () => {
      const isFormValid = await v$.value.$validate();
      if (isFormValid) {
        console.log(state);
        alert("Form is valid.");
      } else {
        console.error(v$.value.$errors);
        alert("Form is invalid.");
      }
    };

    return { state, v$, onSubmitClick };
  },
});
</script>

<style scoped>
#home__container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.form__container {
  width: 400px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.form__container button {
  padding: 10px;
  cursor: pointer;
  text-transform: uppercase;
  letter-spacing: 2px;
}
</style>
