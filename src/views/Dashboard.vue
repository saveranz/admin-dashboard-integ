<template>
    <div class="dashboard">
      <!-- Event Selector -->
      <div class="event-selector">
        <h2>Event Attendance Overview</h2>
        <select v-model="selectedEventId" class="event-dropdown">
          <option v-for="event in events" :key="event.id" :value="event.id">
            {{ event.name }} ({{ event.date }})
          </option>
        </select>
      </div>
  
      <!-- Stats Cards -->
      <div class="stats-container">
        <StatCard 
          title="Present" 
          :value="currentEvent.present" 
          icon="✅" 
          color="#4CAF50" 
        />
        <StatCard 
          title="Late" 
          :value="currentEvent.late" 
          icon="⏰" 
          color="#FFC107" 
        />
        <StatCard 
          title="Absent" 
          :value="currentEvent.absent" 
          icon="❌" 
          color="#F44336" 
        />
      </div>
  
      <!-- Attendance Chart -->
      <div class="chart-container">
        <h3>Attendance for {{ currentEvent.name }}</h3>
        <div class="attendance-bars">
          <div class="bar-container">
            <div class="bar-label">Present</div>
            <div class="bar-bg">
              <div 
                class="bar present" 
                :style="{ width: getPercentage(currentEvent.present) }"
              >
                {{ currentEvent.present }}
              </div>
            </div>
          </div>
          <div class="bar-container">
            <div class="bar-label">Late</div>
            <div class="bar-bg">
              <div 
                class="bar late" 
                :style="{ width: getPercentage(currentEvent.late) }"
              >
                {{ currentEvent.late }}
              </div>
            </div>
          </div>
          <div class="bar-container">
            <div class="bar-label">Absent</div>
            <div class="bar-bg">
              <div 
                class="bar absent" 
                :style="{ width: getPercentage(currentEvent.absent) }"
              >
                {{ currentEvent.absent }}
              </div>
            </div>
          </div>
        </div>
      </div>
  
      <!-- Student Check-ins -->
      <div class="activity-container">
        <h3>Student Attendance Records</h3>
        <div class="student-filters">
          <select v-model="selectedDepartment" class="filter-dropdown">
            <option value="all">All Departments</option>
            <option v-for="dept in departments" :key="dept" :value="dept">
              {{ dept }}
            </option>
          </select>
          <select v-model="selectedStatus" class="filter-dropdown">
            <option value="all">All Statuses</option>
            <option value="present">Present</option>
            <option value="late">Late</option>
            <option value="absent">Absent</option>
          </select>
        </div>
        
        <div class="student-list">
          <div v-for="student in filteredStudents" :key="student.id" class="student-item">
            <span class="status-icon" :class="getAttendanceForEvent(student).status">
              {{ getStatusIcon(getAttendanceForEvent(student).status) }}
            </span>
            <div class="student-info">
              <div class="name-dept">
                <strong>{{ student.name }}</strong>
                <span class="department">{{ student.department }}</span>
              </div>
              <div class="attendance-details">
                <span class="time">{{ getAttendanceForEvent(student).time || 'Not recorded' }}</span>
                <span class="event-name">{{ currentEvent.name }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import StatCard from '@/components/StatCard.vue'
  
  export default {
    components: { StatCard },
    data() {
      return {
        selectedEventId: 1,
        selectedDepartment: 'all',
        selectedStatus: 'all',
        departments: ['CE', 'IT', 'TM', 'HM', 'PolSci'],
        students: [
          { id: 1, name: "Angelica Bejer", department: "CS" },
          { id: 2, name: "Jholand Galicia", department: "IT" },
          { id: 3, name: "Janwin Almanza", department: "CE" },
          { id: 4, name: "Sarah Johnson", department: "TM" },
          { id: 5, name: "David Wilson", department: "CE" },
          { id: 6, name: "Emily Davis", department: "IT" },
          { id: 7, name: "Robert Taylor", department: "IT" }
        ],
        attendanceRecords: [
          // Format: { studentId, eventId, status, time }
          { studentId: 1, eventId: 1, status: "present", time: "8:05 AM" },
          { studentId: 2, eventId: 1, status: "late", time: "8:20 AM" },
          { studentId: 3, eventId: 1, status: "absent", time: "" },
          { studentId: 4, eventId: 1, status: "present", time: "8:10 AM" },
          { studentId: 1, eventId: 2, status: "present", time: "7:30 AM" },
          { studentId: 2, eventId: 2, status: "late", time: "8:15 AM" },
          { studentId: 5, eventId: 2, status: "present", time: "7:45 AM" },
          { studentId: 6, eventId: 3, status: "present", time: "9:00 AM" },
          { studentId: 7, eventId: 3, status: "late", time: "9:25 AM" }
        ],
        events: [
          {
            id: 1,
            name: "IT Day Symposium",
            date: "2023-10-15",
            present: 185,
            late: 12,
            absent: 23
          },
          {
            id: 2,
            name: "Sports Festival",
            date: "2023-11-05",
            present: 320,
            late: 45,
            absent: 15
          },
          {
            id: 3,
            name: "Science Fair",
            date: "2023-11-20",
            present: 210,
            late: 8,
            absent: 12
          }
        ]
      }
    },
    computed: {
      currentEvent() {
        return this.events.find(e => e.id === this.selectedEventId) || this.events[0]
      },
      filteredStudents() {
        return this.students.filter(student => {
          const matchesDept = this.selectedDepartment === 'all' || 
                            student.department === this.selectedDepartment
          const matchesStatus = this.selectedStatus === 'all' || 
                              this.getAttendanceForEvent(student).status === this.selectedStatus
          return matchesDept && matchesStatus
        })
      },
      totalAttendees() {
        return this.currentEvent.present + this.currentEvent.late + this.currentEvent.absent
      }
    },
    methods: {
      getPercentage(value) {
        return `${(value / this.totalAttendees) * 100}%`
      },
      getStatusIcon(status) {
        return {
          present: '✅',
          late: '⏰',
          absent: '❌'
        }[status]
      },
      getAttendanceForEvent(student) {
        const record = this.attendanceRecords.find(
          r => r.studentId === student.id && r.eventId === this.selectedEventId
        )
        return record || { status: 'absent', time: '' }
      }
    }
  }
  </script>
  
  <style scoped>
.dashboard {
  padding: 32px;
  max-width: 1000px;
  margin: 0 auto;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f9fafb;
}

h2, h3 {
  color: #333;
  margin-bottom: 16px;
}

.event-selector {
  background: #ffffff;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.05);
  margin-bottom: 24px;
}

.event-dropdown, .filter-dropdown {
  padding: 10px 14px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 15px;
  margin-right: 12px;
  margin-bottom: 10px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}

.stats-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 20px;
  margin-bottom: 30px;
}

.chart-container,
.activity-container {
  background: #ffffff;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
  margin-bottom: 30px;
}

.attendance-bars {
  margin-top: 20px;
}

.bar-container {
  margin-bottom: 18px;
}

.bar-label {
  margin-bottom: 6px;
  font-weight: 600;
  color: #555;
}

.bar-bg {
  background: #e5e7eb;
  border-radius: 8px;
  height: 36px;
  overflow: hidden;
}

.bar {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding-right: 14px;
  color: #fff;
  font-weight: bold;
  min-width: fit-content;
  border-radius: 8px;
  transition: width 0.6s ease;
}

.present { background-color: #22c55e; }
.late { background-color: #facc15; color: #333; }
.absent { background-color: #ef4444; }

.student-filters {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.student-list {
  margin-top: 10px;
}

.student-item {
  display: flex;
  align-items: center;
  padding: 16px 0;
  border-bottom: 1px solid #e5e7eb;
}

.status-icon {
  font-size: 1.4rem;
  margin-right: 16px;
  width: 30px;
  text-align: center;
}

.present.status-icon { color: #22c55e; }
.late.status-icon { color: #eab308; }
.absent.status-icon { color: #dc2626; }

.student-info {
  flex: 1;
}

.name-dept {
  display: flex;
  align-items: center;
  margin-bottom: 4px;
}

.department {
  background: #f3f4f6;
  padding: 3px 10px;
  border-radius: 9999px;
  font-size: 0.75rem;
  margin-left: 10px;
  color: #4b5563;
}

.attendance-details {
  display: flex;
  font-size: 0.85rem;
  color: #6b7280;
}

.time {
  margin-right: 14px;
}

.event-name {
  font-style: italic;
}

@media (max-width: 768px) {
  .stats-container {
    grid-template-columns: 1fr;
  }

  .student-filters {
    flex-direction: column;
  }

  .filter-dropdown {
    width: 100%;
    margin-right: 0;
    margin-bottom: 12px;
  }
}
</style>