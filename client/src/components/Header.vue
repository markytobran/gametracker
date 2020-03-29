<template>
  <header>
    <img :src="image" />
  </header>
</template>


<script>
export default {
  name: 'Header',
  data() {
    return {
      image: require('@/assets/logo.png')
    };
  }
};
</script>


<style scoped>
img {
  width: 200px;
  height: 200px;
  padding-bottom: 10px;
}

@media (max-width: 700px) {
  img {
    display: block;
    margin: auto;
  }
}
</style>