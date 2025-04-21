<template>
    <div class="activity-feed">
      <div v-for="(item, index) in items" :key="index" class="activity-item">
        <i :class="iconClass(item.type)"></i>
        <div class="details">
          <strong>{{ item.name }}</strong>
          <span>{{ statusText(item.type) }} at {{ item.time }}</span>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      items: Array
    },
    methods: {
      iconClass(type) {
        return {
          'present': 'pi pi-check-circle',
          'late': 'pi pi-clock',
          'absent': 'pi pi-times-circle'
        }[type]
      },
      statusText(type) {
        return {
          'present': 'Checked in',
          'late': 'Arrived late',
          'absent': 'Absent'
        }[type]
      }
    }
  }
  </script>
  
  <style scoped>
  .activity-feed {
    margin-top: 15px;
  }
  .activity-item {
    display: flex;
    align-items: center;
    padding: 10px 0;
    border-bottom: 1px solid #eee;
  }
  .activity-item i {
    font-size: 1.2rem;
    margin-right: 15px;
  }
  .present { color: #4CAF50; }
  .late { color: #FFC107; }
  .absent { color: #F44336; }
  .details {
    display: flex;
    flex-direction: column;
  }
  .details span {
    font-size: 0.9rem;
    color: #666;
  }
  </style>