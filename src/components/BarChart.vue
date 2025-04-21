<template>
    <div class="bar-chart">
      <div class="chart-row" v-for="(label, index) in data.labels" :key="index">
        <div class="label">{{ label }}</div>
        <div class="bars">
          <div class="bar present" :style="{ width: data.present[index] + 'px' }"></div>
          <div class="bar late" :style="{ width: data.late[index] + 'px' }"></div>
          <div class="bar absent" :style="{ width: data.absent[index] + 'px' }"></div>
        </div>
      </div>
      <div class="legend">
        <span><div class="legend-color present"></div> Present</span>
        <span><div class="legend-color late"></div> Late</span>
        <span><div class="legend-color absent"></div> Absent</span>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      data: Object
    }
  }
  </script>
  
  <style scoped>
  .bar-chart {
    margin-top: 20px;
  }
  .chart-row {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }
  .label {
    width: 40px;
    font-weight: 500;
  }
  .bars {
    display: flex;
    gap: 3px;
    flex: 1;
  }
  .bar {
    height: 20px;
    border-radius: 4px;
  }
  .present { background: #4CAF50; }
  .late { background: #FFC107; }
  .absent { background: #F44336; }
  .legend {
    display: flex;
    gap: 15px;
    margin-top: 15px;
    font-size: 0.8rem;
  }
  .legend-color {
    display: inline-block;
    width: 12px;
    height: 12px;
    border-radius: 2px;
    margin-right: 5px;
  }
  </style>