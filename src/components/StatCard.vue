<template>
    <div class="stat-card" :style="{ borderLeft: `4px solid ${color}` }">
      <div class="stat-icon">{{ icon }}</div>
      <div class="stat-value">{{ value }}</div>
      <div class="stat-title">{{ title }}</div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['title', 'value', 'icon', 'color']
  }
  </script>
  
  <style scoped>
  .stat-card {
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  }
  .stat-icon {
    font-size: 2rem;
    margin-bottom: 10px;
  }
  .stat-value {
    font-size: 2rem;
    font-weight: bold;
    margin: 5px 0;
  }
  .stat-title {
    color: #666;
    font-size: 0.9rem;
  }
  </style>