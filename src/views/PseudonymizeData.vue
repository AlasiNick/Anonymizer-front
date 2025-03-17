<template>
    <BaseLayout>
      <div class="home-content">
        <h1>Welcome to Pseudonym</h1>
        <p>Your trusted partner in data processing and risk assessment.</p>
      </div>
    </BaseLayout>
  </template>
  
  <script>
  import BaseLayout from '../layouts/BaseLayout.vue';
  
  export default {
    name: 'PsuedonymizeData',
    components: {
      BaseLayout,
    },
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