<template>
  <div id="home__container">
    <form class="form__container">
      <input class="input-text" type="text" placeholder="user id" />
      <input class="input-text" type="text" placeholder="username" />
      <input class="input-text" type="password" placeholder="password" />
      <input
        class="input-text"
        type="password"
        placeholder="confirm password"
      />
      <div class="input-gender__container">
        <div class="input-gender__wrapper">
          <label for="input-gender-male">MALE</label>
          <input id="input-gender-male" type="radio" value="MALE" />
        </div>
        <div class="input-gender__wrapper">
          <label for="input-gender-female">FEMALE</label>
          <input id="input-gender-female" type="radio" value="FEMALE" />
        </div>
      </div>

      <div class="input-selector__container">
        <select class="input-selector">
          <option disabled value="">Please select one</option>
          <option>A</option>
          <option>B</option>
          <option>C</option>
        </select>
      </div>

      <button type="submit">submit</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "HomeView",
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
.form__container .input-text {
  padding: 10px;
}
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
.form__container .input-selector {
  width: 100%;
  padding: 10px;
}
.form__container button {
  padding: 10px;
  cursor: pointer;
  text-transform: uppercase;
  letter-spacing: 2px;
}
</style>
