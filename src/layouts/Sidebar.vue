<template>
  <div class="sidebar">
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
</template>

<script>
export default {
  name: "Sidebar",
};
</script>

<style scoped>
.sidebar {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 20px;
  background: linear-gradient(180deg, #3865F2 39%, #161C60 100%);
  height: 100vh;
  width: 450px;
}

.icon_top img {
  width: 250px;
  height: 100px;
  margin-top: 25px;
  margin-bottom: 50px;
}

.sidebar-item {
  display: flex;
  align-items: center;
  text-decoration: none;
  color: white;
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 15px;
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
}

.icon {
  width: 60px;
  height: 30px;
  margin-right: 10px;
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
}

.sub-items {
  margin-left: 111px;  
}

.sub-item {
  font-family: 'Montserrat', sans-serif;
  font-size: 24px;
  color: white;
  text-decoration: none;
  display: block;
  margin-bottom: 10px;
}

.sub-item::before {
  content: '\2022'; /* Unicode for a centered bullet point */
  font-size: 18px;
  margin-right: 10px;
  color: white;
}

.sub-item:hover {
  text-decoration: solid;
}
</style>

  