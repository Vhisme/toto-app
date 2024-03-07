<template>
  <div class="container">
    <h2 class="text-container mt-5">My Todo App</h2>

    <!-- Input -->
    <div class="d-flex mt-5">
      <input v-model="task" placeholder="Enter task" class="w-100 form-control">
      <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <!-- Task table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{ 'line-through': task.status === 'finished' }">{{ task.name }}</span>
          </td>
          <td>
            <span class="pointer noselect"
                  @click="changeStatus(index)"
                  :class="{
                    'text-danger': task.status === 'to-do',
                    'text-success': task.status === 'finished',
                    'text-warning': task.status === 'in-progress',
                  }">
              {{ capitalizeFirstChar(task.status) }}
            </span>
          </td>
          <td class="text-center">
            <div @click="editTask(index)" class="btn btn-warning">Edit
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
            <td class="text-center">
            <!-- New button to delete the task -->
            <button @click="deleteTask(index)" class="btn btn-danger">Delete</button>
          </td>
            </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      task: "",
      editedTask: null,
      statuses: ["to-do", "in-progress", "finished"],
      tasks: [
        { name: "Steal bananas from the supermarket.", status: "to-do" },
        { name: "Eat 1 kg chocolate in 1 hour.", status: "in-progress" },
        { name: "Create YouTube video.", status: "finished" },
      ],
    };
  },
  methods: {
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },
    deleteTask(index) {
      if (confirm("Are you sure you want to delete this task?")) {
      this.tasks.splice(index, 1);
    }
  },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    submitTask() {
      if (this.task.length === 0) return;

      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        this.tasks.push({ name: this.task, status: "to-do" });
      }

      this.task = "";
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.noselect {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.line-through {
  text-decoration: line-through;
  border-radius: 1.2rem;
  text-align: center;
  text-transform: non;
  color: rgb(20, 72, 202);
}
.container {
  background-color: aqua;
  text-decoration: antiquewhite;
  color: rgba(104, 30, 233, 0.114);
  border-style:var(-webkit-touch-callout);
}

</style>
