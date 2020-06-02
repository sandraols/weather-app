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
  // animation: timelaps 5s infinite;
  // animation-timing-function: linear;
}
.header__container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 70vw;
  height: 40vh;
}
.main__title {
  font-family: "Rubik", sans-serif;
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
  font-family: "Roboto", sans-serif;
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
    #ffba65 21.58%,
    rgba(255, 160, 160, 0) 67.08%
  );
  border-radius: 50%;
  position: absolute;
  bottom: -40%;
  right: -30%;
  z-index: -1;
}
// @keyframes timelaps {
// 0% {
//   background: linear-gradient(180deg, #83a5ff 0%, #ffdffc 100%);
// }
// 10% {
//   background: linear-gradient(180deg, #a7beff 0%, #ffcce4 100%);
// }
// 20% {
//   background: linear-gradient(180deg, #657dbe 0%, #daa1bb 100%);
// }
// 30% {
//   background: linear-gradient(180deg, #3b4e83 0%, #b88080 100%);
// }
// 40% {
//   background: linear-gradient(180deg, #0d1529 0%, #735888 100%);
// }
// 50% {
//   background: linear-gradient(180deg, #421f4b 0%, #f18b79 100%);
// }
// 60% {
//   background: linear-gradient(180deg, #c887d8 0%, #ffbeb3 100%);
// }
// 70% {
//   background: linear-gradient(180deg, #f4c6ff 0%, #ffe4b1 100%);
// }
// 80% {
//   background: linear-gradient(180deg, #dac6ff 0%, #ffcab1 100%);
// }
// 90% {
//   background: linear-gradient(180deg, #b7b8ff 0%, #ecb5b5 100%);
// }
// 100% {
//   background: linear-gradient(180deg, #83a5ff 0%, #ffdffc 100%);
// }
// }
@media only screen 
and (min-device-width : 768px) 
and (max-device-width : 1024px)  { 
    .header__container {
    height: 23vh;
  }
}
@media screen and (max-width: 590px) {
  .input {
    position: relative;
    z-index: 1;
    align-self: center;
  }
  .main__title {
    font-size: 11vw;
  }
}
@media screen and (max-width: 414px) {
  .header__container {
    height: 32vh;
    width: fit-content;
  }
  .sun {
    bottom: -90%;
    right: -24%;
  }
}
@media only screen and (min-device-width: 414px) and (max-device-width: 736px) {
  .header__container {
    height: 43vh;
    width: 66vw;
  }
}
@media only screen and (min-device-width: 375px) and (max-device-width: 667px) {
  .header__container {
    height: 38vh;
  }
}
@media only screen and (min-device-width: 320px) and (max-device-width: 568px) {
  .header__container {
    height: 40vh;
    width: 58vw;
  }
}
</style>
