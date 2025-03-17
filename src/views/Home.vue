<template>
  <BaseLayout>
    <h1>Home Page</h1>
  </BaseLayout>
</template>
<script>
import BaseLayout from '../layouts/BaseLayout.vue';
export default {
  name: "Home",
  components: { BaseLayout },
};
</script>
  
  <style scoped>
  .home-content {
    text-align: center;
    padding: 20px;
  }
  
  h1 {
    font-family: 'Montserrat', sans-serif;
    font-weight: 600;
    font-size: 48px;
    color: #333;
  }
  
  p {
    font-family: 'Montserrat', sans-serif;
    font-weight: 400;
    font-size: 24px;
    color: #666;
    margin-top: 20px;
  }
  </style>