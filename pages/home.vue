<template>
  <div>
    <Nav></Nav>
    <nuxt-child></nuxt-child>
  </div>
</template>
 <script>
export default {
  mounted() {
    this.$router.replace("/home/dashboard");
  },
};
</script>