<template>
    <div>
        <div v-if="showAddTask">
            <AddTask @add-task="addTask" />
        </div>
        <Tasks @toggle-reminder="toggleRemainder" @delete-task="deleteTask" :tasks="tasks"/>
    </div>
</template>
<script>

import Tasks from '../components/Tasks.vue';
import AddTask from '../components/AddTask.vue';

export default {
  name: 'Home',
  components: {
    Tasks,
    AddTask,
  },
  props: [
    'showAddTask',
  ],
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: 'DELETE',
        headers:
        {
          'Content-Type': 'application/json',
        },
      });
      switch (res.status) {
        case 200:
          this.tasks = this.tasks.filter((item) => (item.id !== id));
          break;
        default:
          alert('something gone wrong');
      }
    },

    async toggleRemainder(id) {
      const taskToToggle = await this.fetchTaskId(id);
      taskToToggle.reminder = !taskToToggle.reminder;
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers:
        {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(taskToToggle),
      });
      switch (res.status) {
        case 200:
        { const index = this.tasks.findIndex((taskItem) => (taskItem.id === id));
          this.tasks[index] = taskToToggle;
          break; }
        default:
          alert('something happend unexpectedly');
      }
    },

    async fetchTask() {
      const res = await fetch('api/tasks');
      const data = await res.json();
      return data;
    },
    async fetchTaskId(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: 'GET',
        headers:
        {
          'Content-Type': 'application/json',
        },
      });
      const data = await res.json();
      return data;
    },
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers:
        {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      this.tasks = [
        ...this.tasks,
        data,
      ];
    },
  },

  async created() {
    this.tasks = await this.fetchTask();
  },
};
</script>

<style scoped>
.container { max-width: 500px; margin: 30px auto;
overflow: auto; min-height: 300px; border: 1px solid steelblue; padding: 30px;
border-radius: 5px; }
</style>
