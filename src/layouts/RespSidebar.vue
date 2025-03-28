<template>
    <div class="sidebar" :class="{ 'sidebar--collapsed': isCollapsed }">
      <div class="icon_top mb-xxl">
        <img src="../assets/cyberwiseLogo.svg" alt="Cyberwise" />
      </div>
      
      <router-link to="/" class="sidebar-item">
        <img src="../assets/home.svg" alt="Home" class="icon" />
        <span class="icon-text">Home</span>
      </router-link>
      
      <div class="data-processing">
        <div class="sidebar-item-data">
          <img src="../assets/dataprocessing.svg" alt="Data processing" class="icon" />
          <span class="icon-text">Data Processing</span>
        </div>
        <div class="sub-items">
          <router-link to="/anonymize" class="sub-item">Anonymize data</router-link>
          <router-link to="/pseudonymize" class="sub-item">Pseudonymize data</router-link>
          <router-link to="/projects" class="sub-item">My projects</router-link>
        </div>
      </div>
      
      <router-link to="/risk-assessment" class="section-title">Risk assessment</router-link>
    </div>
    <button class="mobile-toggle" @click="toggleSidebar">
      <span class="mobile-toggle__icon"></span>
    </button>
  </template>
  
  <script>
  export default {
    name: "Sidebar",
    data() {
      return {
        isCollapsed: false
      };
    },
    watch: {
      '$route'() {
        // Close sidebar on route change
        this.isCollapsed = false;
      }
    },
    methods: {
      toggleSidebar() {
        this.isCollapsed = !this.isCollapsed;
      }
    },
    mounted() {
      // Start with sidebar closed
      this.isCollapsed = false;
    }
  };
  </script>
  
  <style scoped>
  .sidebar {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    padding: 24px 20px;
    background: linear-gradient(180deg, #3865F2 39%, #161C60 100%);
    height: 100vh;
    width: 450px;
    position: fixed;
    left: 0;
    top: 0;
    z-index: 2;
    overflow-y: auto;
    transition: all 0.3s ease;
    transform: translateX(-100%);
    box-shadow: none;
  
    &.sidebar--collapsed {
      transform: translateX(0);
      box-shadow: 2px 0 10px rgba(0, 0, 0, 0.1);
    }
  
    @media (max-width: 768px) {
      width: 300px;
    }
  }
  
  .mobile-toggle {
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    left: 20px;
    top: 20px;
    background: rgba(56, 101, 242, 0.9);
    backdrop-filter: blur(8px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    width: 44px;
    height: 44px;
    cursor: pointer;
    z-index: 1000;
    border-radius: 12px;
    transition: all 0.3s ease;
    box-shadow: 
      0 4px 12px rgba(0, 0, 0, 0.1),
      0 2px 4px rgba(56, 101, 242, 0.2);
  
    .sidebar--collapsed & {
      left: calc(450px - 64px);
      background: rgba(22, 28, 96, 0.9);
  
      @media (max-width: 768px) {
        left: calc(300px - 64px);
      }
    }
  
    &:hover {
      transform: translateY(-2px);
      background: rgba(56, 101, 242, 1);
      box-shadow: 
        0 8px 24px rgba(0, 0, 0, 0.15),
        0 4px 8px rgba(56, 101, 242, 0.3);
    }
  
    &:active {
      transform: translateY(1px);
    }
  
    &__icon {
      width: 18px;
      height: 2px;
      background: white;
      position: relative;
      border-radius: 1px;
      transition: all 0.3s ease;
  
      &::before,
      &::after {
        content: '';
        position: absolute;
        width: 100%;
        height: 100%;
        background: white;
        left: 0;
        border-radius: 1px;
        transition: all 0.3s ease;
      }
  
      &::before {
        top: -5px;
      }
  
      &::after {
        bottom: -5px;
      }
    }
  
    .sidebar--collapsed & {
      &__icon {
        background: transparent;
  
        &::before {
          top: 0;
          transform: rotate(45deg);
        }
  
        &::after {
          bottom: 0;
          transform: rotate(-45deg);
        }
      }
    }
  }
  
  .icon_top img {
    width: 250px;
    height: 100px;
    margin-top: 25px;
    margin-bottom: 50px;
  
    @media (max-width: 992px) {
      width: 180px;
      height: 80px;
    }
  
    @media (max-width: 768px) {
      width: 160px;
      height: 70px;
    }
  }
  
  .sidebar-item {
    display: flex;
    align-items: center;
    text-decoration: none;
    color: white;
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 15px;
  
    @media (max-width: 768px) {
      font-size: 20px;
    }
  }
  
  .sidebar-item-data {
    display: flex;
    align-items: center;
    text-decoration: none;
    color: white;
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 15px;
    margin-top: 40px;
  
    @media (max-width: 768px) {
      font-size: 20px;
    }
  }
  
  .icon {
    width: 60px;
    height: 30px;
    margin-right: 10px;
  
    @media (max-width: 768px) {
      width: 40px;
      height: 20px;
    }
  }
  
  .section-title {
    font-family: 'Montserrat', sans-serif;
    font-size: 24px;
    color: white;
    margin-bottom: 15px;
    margin-top: 50px;
    text-decoration: none;
    font-weight: bold;
    margin-left: 90px;
  
    @media (max-width: 768px) {
      font-size: 20px;
      margin-left: 60px;
    }
  }
  
  .sub-items {
    margin-left: 111px;
  
    @media (max-width: 768px) {
      margin-left: 70px;
    }
  }
  
  .sub-item {
    font-family: 'Montserrat', sans-serif;
    font-size: 24px;
    color: white;
    text-decoration: none;
    display: block;
    margin-bottom: 10px;
  
    @media (max-width: 768px) {
      font-size: 18px;
    }
  
    &::before {
      content: '\2022';
      font-size: 18px;
      margin-right: 10px;
      color: white;
    }
  
    &:hover {
      text-decoration: solid;
    }
  }
  </style>
  
    