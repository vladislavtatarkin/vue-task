<template>
  <div>
    <h1>List</h1>

    <div class="row">
      <div class="input-field col s6 ">
        <select ref="select" v-model="filter">
          <option value="" disabled selected>Choose your option</option>
          <option value="active">Active</option>
          <option value="outdated">Outdated</option>
          <option value="completed">Completed</option>
        </select>
        <label>Status filter</label>
      </div>
    </div>

    <button v-if="filter" class="btn btn-small red" @click="filter = null">Clear filter</button>

    <hr>

    <table v-if="tasks.length">
      <thead>
      <tr>
        <th>#</th>
        <th>Title</th>
        <th>Date</th>
        <th>Description</th>
        <th>Status</th>
        <th>Open</th>
      </tr>
      </thead>
      <tbody>
      <tr
          v-for="(task, idx) of displayTasks"
          :key="task.id"
      >
        <td>{{ idx + 1 }}</td>
        <td>{{ task.title }}</td>
        <td>{{ new Date(task.date).toLocaleDateString() }}</td>
        <td class="td">
          <div class="text">{{ task.description }}</div>
        </td>
        <td>
          <span
              :class="task.status === 'active'
              ? 'status active'
              : task.status === 'completed'
              ? 'status completed'
              : task.status === 'outdated'
              ? 'status outdated'
              : null
              "
          >
            {{ task.status }}
          </span>
        </td>
        <td>
          <router-link tag="button" class="btn btn-small" :to="'/task/' + task.id">
            Open
          </router-link>
        </td>
      </tr>
      </tbody>
    </table>
    <p v-else>No tasks</p>
  </div>
</template>

<script>
export default {
  data: () => ({
    filter: null
  }),
  computed: {
    tasks() {
      return this.$store.getters.tasks
    },
    displayTasks() {
      return this.tasks.filter(t => {
        if (!this.filter) {
          return true
        }
        return t.status === this.filter
      })
    }
  },
  mounted() {
    M.FormSelect.init(this.$refs.select)
  }
}
</script>

<style lang="css" scoped>
  .td {
    max-width: 400px;
  }

  .text {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }

  .status {
    color: white;
    padding: 6px 10px;
  }
  .status.active {
    background-color: #1e88e5;
  }

  .status.completed {
    background-color: #00897b;
  }

  .status.outdated {
    background-color: #e53935;
  }
</style>