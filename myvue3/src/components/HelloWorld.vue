
<template>
  <div id="app">
    <body>
      <h1>ToDoリスト</h1>
      <label
        ><input
          type="radio"
          name="list"
          value="all"
          v-model="filter"
        />すべて</label
      >
      <label
        ><input
          type="radio"
          name="list"
          value="active"
          v-model="filter"
        />作業中</label
      >
      <label
        ><input
          type="radio"
          name="list"
          value="completed"
          v-model="filter"
        />完了</label
      >

      <table>
        <tr v-for="(todo, key) in filteredTodos" :key="key">
          <td>{{ todo.id }}</td>
          <td>{{ todo.title }}</td>
          <td>
            <button @click="statusChange(todo.id)">
              <span>{{ todo.statusBtn }}</span>
            </button>
          </td>
          <td>
            <button @click="deleteTask(todo.id)">{{ todo.delBtn }}</button>
          </td>
        </tr>
      </table>

      <h2>新規タスクの追加</h2>
      <form @submit.prevent="addTask">
        <input type="text" v-model="newTask" />
        <input type="submit" value="追加" class="button" />
      </form>
    </body>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: 0,
      statusBtn: "",
      newTask: "",
      todos: [],
      filter: "all",
    };
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      } else if (this.filter === "completed") {
        return this.todos.filter((todo) => {
          return todo.statusBtn === "完了";
        });
      } else if (this.filter === "active") {
        return this.todos.filter((todo) => {
          return todo.statusBtn === "作業中";
        });
      } else {
        return this.todo.statusBtn === "";
      }
    },
  },
  methods: {
    addTask: function () {
      let item = {
        id: this.id++,
        title: this.newTask,
        statusBtn: "作業中",
        delBtn: "削除",
      };
      this.todos.push(item);
      this.newTask = "";
    },
    statusChange: function (id) {
      this.todos.forEach(function (todo) {
        if (todo.id === id) {
          if (todo.statusBtn === "作業中") {
            todo.statusBtn = "完了";
          } else {
            todo.statusBtn = "作業中";
          }
        }
      });
    },
    deleteTask: function (index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>