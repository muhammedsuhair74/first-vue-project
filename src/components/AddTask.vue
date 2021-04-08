<template>
    <div class="add-form">
        <form @submit="onSubmit">
            <div class="form-control">
                <label>Text </label>
                <input v-model="text" name="text" type="text" placeholder="text"/>
            </div>
            <div class="form-control">
                <label>Day and time </label>
                <input v-model="day" name="day" type="text" placeholder="day"/>
            </div>
            <div class="form-control form-control-check">
                <label>Set Reminder </label>
                <input v-model="reminder" name="reminder" type="checkbox"/>
            </div>
            <input type="submit" value="Save Task" class="btn btn-block" />
        </form>
    </div>
</template>
<script>

export default ({
  name: 'AddTask',
  data() {
    return {
      id: '',
      text: '',
      day: '',
      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.text) {
        alert('please add some text');
        return;
      }
      const data = {
        text: this.text,
        day: this.day,
        reminder: this.reminder,
      };
      this.$emit('add-task', data);
      this.text = '';
      this.day = '';
      this.reminder = false;
    },
  },
});
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
