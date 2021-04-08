,<template>
    <header>
        <h1>{{title}}</h1>
        <Button v-show="homePage"  @btn-click="$emit('toggle-showAddTask')"
        :text="showAddTask ? 'close' : 'Add Task'" :color="showAddTask ? 'red' :'green' "/>
    </header>
</template>

<script>
import Button from './Button.vue';

export default {
  name: 'Header',
  components: {
    Button,
  },
  computed: {
    homePage() {
      if (this.$route.path === '/') {
        return true;
      }
      return false;
    },
  },
  props: ['title', 'showAddTask'],
};
</script>

<style scoped>
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>
