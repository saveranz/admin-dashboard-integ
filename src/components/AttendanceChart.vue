<template>
    <div class="chart-card">
      <h3>{{ event.name }} Attendance by Category</h3>
      <div class="chart">
        <div v-for="(category, index) in event.attendanceData.labels" 
             :key="category" 
             class="chart-row">
          <div class="category-label">{{ category }}</div>
          <div class="bars">
            <div class="bar present" 
                 :style="{ width: getBarWidth(event.attendanceData.present[index]) }"
                 :title="Present: ${event.attendanceData.present[index]}"></div>
            <div class="bar late" 
                 :style="{ width: getBarWidth(event.attendanceData.late[index]) }"
                 :title="Late: ${event.attendanceData.late[index]}"></div>
            <div class="bar absent" 
                 :style="{ width: getBarWidth(event.attendanceData.absent[index]) }"
                 :title="Absent: ${event.attendanceData.absent[index]}"></div>
          </div>
          <div class="total">
            {{ event.attendanceData.present[index] + event.attendanceData.late[index] }}
          </div>
        </div>
      </div>
      <div class="legend">
        <div v-for="item in legend" :key="item.label" class="legend-item">
          <span class="legend-color" :style="{ backgroundColor: item.color }"></span>
          {{ item.label }}
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      event: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        legend: [
          { label: 'Present', color: '#4CAF50' },
          { label: 'Late', color: '#FFC107' },
          { label: 'Absent', color: '#F44336' }
        ]
      }
    },
    methods: {
      getBarWidth(value) {
        const maxValue = Math.max(...this.event.attendanceData.present)
        return ${(value / maxValue) * 100}%
      }
    }
  }
  </script>
  
  <style scoped>
  .chart-card {
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    height: 100%;
  }
  
  h3 {
    margin-top: 0;
    color: #2e7d32;
    margin-bottom: 20px;
  }
  
  .chart {
    margin-top: 10px;
  }
  
  .chart-row {
    display: flex;
    align-items: center;
    margin-bottom: 12px;
  }
  
  .category-label {
    width: 80px;
    font-weight: 500;
    font-size: 0.9rem;
  }
  
  .bars {
    flex: 1;
    display: flex;
    height: 20px;
    gap: 3px;
    margin: 0 15px;
  }
  
  .bar {
    border-radius: 4px;
    transition: width 0.3s ease;
  }
  
  .present { background: #4CAF50; }
  .late { background: #FFC107; }
  .absent { background: #F44336; }
  
  .total {
    width: 40px;
    text-align: right;
    font-weight: bold;
    font-size: 0.9rem;
  }
  
  .legend {
    display: flex;
    gap: 15px;
    margin-top: 20px;
    flex-wrap: wrap;
  }
  
  .legend-item {
    display: flex;
    align-items: center;
    font-size: 0.8rem;
  }
  
  .legend-color {
    width: 12px;
    height: 12px;
    border-radius: 2px;
    margin-right: 5px;
  }
  </style>