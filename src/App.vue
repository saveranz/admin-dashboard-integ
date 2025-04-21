<template>
  <div class="app-container">
    <!-- New Header Design -->
    <header class="university-header">
      <div class="header-content">
        <div class="logo-space">
          <!-- Space for logo (add your logo file here) -->
          <img v-if="false" src="@/assets/university-logo.png" alt="University Logo" class="logo">
          <div v-else class="logo-placeholder"></div>
        </div>
        <div class="university-info">
          <h1 class="university-name">Mindoro State University - Bongabong Campus</h1>
          <h2 class="system-title">Student Attendance System</h2>
        </div>
      </div>
      <div class="header-bottom-bar"></div>
    </header>

    <main class="dashboard">
      <DashboardView />
    </main>
  </div>
</template>

<script>
import DashboardView from './views/Dashboard.vue'

export default {
  components: { DashboardView }
}
</script>

<style>
/* Base Styles */
body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: #f8f9fa;
}

.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* New Header Styles */
.university-header {
  background: linear-gradient(135deg, #2e7d32 0%, #1b5e20 100%);
  color: white;
  padding: 1rem 0 0 0;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  position: relative;
}

.header-content {
  display: flex;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.logo-space {
  width: 80px;
  height: 80px;
  margin-right: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.logo {
  max-width: 100%;
  max-height: 100%;
}

.logo-placeholder {
  width: 60px;
  height: 60px;
  border: 2px dashed rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.8rem;
}

.university-info {
  flex: 1;
}

.university-name {
  margin: 0;
  font-size: 1.4rem;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.system-title {
  margin: 5px 0 0 0;
  font-size: 1.1rem;
  font-weight: 400;
  opacity: 0.9;
}

.header-bottom-bar {
  height: 4px;
  background: linear-gradient(90deg, #ffc107 0%, #f57f17 100%);
  margin-top: 1rem;
}

.dashboard {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
  flex: 1;
  width: 100%;
}

/* Responsive Adjustments */
@media (max-width: 768px) {
  .header-content {
    flex-direction: column;
    text-align: center;
    padding-bottom: 10px;
  }
  
  .logo-space {
    margin-right: 0;
    margin-bottom: 10px;
  }
  
  .university-name {
    font-size: 1.2rem;
  }
  
  .system-title {
    font-size: 1rem;
  }
}
</style>