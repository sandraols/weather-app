<template>
  <header class="header">
    <div class="header__container">
      <h1 class="main__title">
        How's the
        <br>weather?
        <div class="sun"></div>
      </h1>
      <input
        v-on:keyup.enter="$emit('getWeather')"
        :value="city"
        v-on:input="$emit('input', $event.target.value)"
        class="input"
        type="text"
        placeholder="How's the weather in..."
      >
    </div>
  </header>
</template>

<script>
export default {
  name: "FirstPage",
  props: {
    city: String
  }
};
</script>

<style lang="scss">
.header {
  height: 100vh;
  width: 100vw;
  background: linear-gradient(180deg, #83a5ff 0%, #ffdffc 100%);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.header__container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 70vw;
  height: 40vh;
}

.main__title {
  font-family: 'Rubik', sans-serif;
  font-size: 78px;
  color: white;
  text-transform: uppercase;
  position: relative;
  z-index: 1;
  width: fit-content;
}

.input {
  background: transparent;
  border: 1px solid white;
  border-radius: 30px;
  font-family: 'Roboto', sans-serif;
  color: white;
  font-size: 14px;
  padding: 10px;
  width: 225px;
}

.input::placeholder {
  color: white;
}

.input:focus {
  outline: none;
}

.sun {
  width: 300px;
  height: 300px;
  background: linear-gradient(
    309.22deg,
    #ffc164 21.58%,
    rgba(255, 160, 160, 0) 67.08%
  );
  border-radius: 50%;
  position: absolute;
  bottom: -40%;
  right: -30%;
  z-index: -1;
}
</style>
