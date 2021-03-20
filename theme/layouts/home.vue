<template>
  <div style="text-align:center;">
    <div>{{ isDark ? 'dark' : 'light' }}</div>
    <button @click="toggleDark">toggle</button>

    <br />
    <button>
      <router-link to="/post.html">post</router-link>
    </button>
  </div>
</template>

<script>
import { useDark, useToggle } from "@vueuse/core";
import { watchEffect } from "vue";
import { usePageData } from '@vuepress/client'

export default {
  name: "Home",

  setup() {
    const pageData = usePageData()

    const isDark = useDark({
      selector: "body",
      attribute: "class",
      valueDark: "dark",
      valueLight: "light",
    });
    const toggleDark = useToggle(isDark);

    watchEffect(() => {
      console.log("isDark", isDark.value);
    });

    return {
      isDark,
      toggleDark
    }
  },
};
</script>

<style>
.dark {
  background: #000;
  color: #fff;
}

.light {
  color: #000;
  background: #fff;
}
</style>
