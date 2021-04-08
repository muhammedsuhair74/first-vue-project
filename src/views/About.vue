<template>
    <div>
        <h1>Versio 1.0.0</h1>
        <div v-for="task in tasks" :key="task.id">
          <div class="loop" v-for="(item,key,index) in task" :key="index">
            <ul>{{key}} :</ul>
            <ul>{{item}}</ul>
          </div>
        </div>
        <router-link to="/">Go Back</router-link>
    </div>
</template>
<script>

export default ({
  name: 'About',
  data() {
    return {
      tasks: [
        {
          id: '1',
          text: 'Doctor Appoinment',
          day: 'March 1st at 2:30pm',
          reminder: false,
        },
        {
          id: '2',
          text: 'Meeting at School',
          day: 'March 3rd at 1:30pm',
          reminder: true,
        },
        {
          id: '3',
          text: 'Food Shopping',
          day: 'March 3rd at 11:00am',
          reminder: false,
        },
        {
          id: '5',
          text: 'Meeting at office',
          day: 'March 3rd at 3:30pm',
          reminder: true,
        },
      ],
    };
  },
});
</script>
<style scoped>
.loop{
  display: flex;
}
</style>
