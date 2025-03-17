<template>
    <div class="base-layout">
      <Sidebar />
      <main class="content">
        <slot></slot> <!-- renders the page-specific content -->
      </main>
    </div>
  </template>
  
  <script>
  import Sidebar from '../layouts/Sidebar.vue'; 
  
  export default {
    name: 'BaseLayout',
    components: {
      Sidebar,
    },
  };
  </script>
  
  <style scoped>
  .base-layout {
    display: flex;
    min-height: 100vh; 
    background-color: #F5F5F5; 
  }
  
  .content {
  flex-grow: 1;
  padding: 40px;
  margin-left: 400px;
  overflow-y: auto;
  display: flex;
  justify-content: center;
  align-items: flex-start; 
  padding-top: 80px; 
}

  </style>