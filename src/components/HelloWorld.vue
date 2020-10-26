<template>
  <h1 class="title-vue">
    <img class="logo" alt="Vue logo" src="../assets/logo.png" />
    {{ msg }}
    <!-- <button @click="count++">count is: {{ count }}</button> -->
  </h1>
  <!-- <p>
    Edit
    <code>components/HelloWorld.vue</code> to test hot module replacement.
  </p> -->
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      count: 0,
    };
  },
};
</script>
<style scoped>
.title-vue {
  display: flex;
  justify-content: center;
}
.logo {
  width: 40px;
  height: 40px;
}
</style>
