<template>
    <div class="activity-card">
      <h3>Recent Activity</h3>
      <div class="activity-list">
        <div v-for="(item, index) in activities" :key="index" class="activity-item">
          <span class="activity-icon" :style="{ color: getColor(item.type) }">
            {{ getIcon(item.type) }}
          </span>
          <div class="activity-details">
            <div class="student">{{ item.student }}</div>
            <div class="time">{{ item.time }}</div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        activities: [
          { student: 'John Doe', type: 'present', time: 'Checked in at 8:05 AM' },
          { student: 'Jane Smith', type: 'late', time: 'Arrived at 8:20 AM' },
          { student: 'Mike Johnson', type: 'absent', time: 'Marked absent' },
          { student: 'Sarah Williams', type: 'penalty', time: 'Late penalty assigned' }
        ]
      }
    },
    methods: {
      getIcon(type) {
        const icons = {
          present: '✅',
          late: '⏰',
          absent: '❌',
          penalty: '⚠️'
        }
        return icons[type] || 'ℹ️'
      },
      getColor(type) {
        const colors = {
          present: '#4CAF50',
          late: '#FFC107',
          absent: '#F44336',
          penalty: '#9C27B0'
        }
        return colors[type] || '#666'
      }
    }
  }
  </script>
  
  <style scoped>
  .activity-card {
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    height: 100%;
  }
  h3 {
    margin-top: 0;
    color: #2e7d32;
  }
  .activity-list {
    margin-top: 15px;
  }
  .activity-item {
    display: flex;
    align-items: center;
    padding: 10px 0;
    border-bottom: 1px solid #eee;
  }
  .activity-icon {
    font-size: 1.2rem;
    margin-right: 15px;
    width: 24px;
    text-align: center;
  }
  .student {
    font-weight: 500;
  }
  .time {
    font-size: 0.8rem;
    color: #666;
  }
  </style>