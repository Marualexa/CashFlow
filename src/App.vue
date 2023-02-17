<template>
  <div>
    <Suspense>
      <template #default>
        <Home />
      </template>
      <template #fallback>
        <SplashScreen />
      </template>
    </Suspense>
  </div>
</template>

<script>
import SplashScreen from "./components/SplashScreen.vue";
import { defineAsyncComponent } from "vue";

export default {
  components: {
    SplashScreen,
    Home: defineAsyncComponent(() => 
      new Promise((resolve) => {
        setTimeout(() => {
          resolve(import("./components/HomeMain.vue"))
        }, 2500);
      })
    )
  },
};
</script>

<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  background-color: #EEEEEE;
}

* {
  --text-color: #E5E5CB;
  --backgrount-1: #205295;
  --backgrount-2: #2c74B3;
}
</style>
