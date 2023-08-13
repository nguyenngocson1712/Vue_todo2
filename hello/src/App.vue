<template>
  <id id="app">
    <div class="row">
      <div class="col-2">
  Tasks
</div>
      <div class="col-2 offset-6">
        <button type="button" class="btn btn-danger" @click="clickAdd">
          Add +
        </button>
      </div>
    </div>
    <div class="todo-list">
      
      <table class="table p-3 bg-white rounded-lg shadow">
        <thead>
          <tr>
            <th
              class="border p-3 dark:border-dark-5 whitespace-nowrap font-bold text-gray-900"
            >
              ID
            </th>
            <th
              class="border p-3 dark:border-dark-5 whitespace-nowrap font-bold text-gray-900"
            >
              Work name
            </th>
            <th
              class="border p-3 dark:border-dark-5 whitespace-nowrap font-bold text-gray-900"
            >
              Action
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in todoL" :key="item.id" class="text-gray-700">
            <td class="border p-3 dark:border-dark-5">
              {{ item.id }}
            </td>
            <td class="border p-3 dark:border-dark-5">
              {{ item.workName }}
            </td>
            <td class=" border p-3 dark:border-dark-5">
              <button  @click="removeTodo(item.id)"
                class="px-3 py-2 bg-rose-500 hover:bg-rose-800 rounded-md drop-shadow-md"
              >
                <svg
                  class="fill-white"
                  xmlns="http://www.w3.org/2000/svg"
                  x="0px"
                  y="0px"
                  width="20"
                  height="20"
                  viewBox="0 0 24 24"
                >
                  <path
                    d="M 10 2 L 9 3 L 3 3 L 3 5 L 21 5 L 21 3 L 15 3 L 14 2 L 10 2 z M 4.3652344 7 L 5.8925781 20.263672 C 6.0245781 21.253672 6.877 22 7.875 22 L 16.123047 22 C 17.121047 22 17.974422 21.254859 18.107422 20.255859 L 19.634766 7 L 4.3652344 7 z"
                  ></path>
                </svg>
                <span class="text-white">Delete</span>
              </button>
              <button 
              @click="clickEdit(item)"
                class="mx-10 items-center px-4 py-2 bg-green-600 hover:bg-amber-600 rounded-full drop-shadow-md"
              >
              
                <svg
                  class="fill-white"
                  xmlns="http://www.w3.org/2000/svg"
                  x="0px"
                  y="0px"
                  width="20"
                  height="20"
                  viewBox="0 0 50 50"
                >
                  <path
                    d="M 46.574219 3.425781 C 45.625 2.476563 44.378906 2 43.132813 2 C 41.886719 2 40.640625 2.476563 39.691406 3.425781 C 39.691406 3.425781 39.621094 3.492188 39.53125 3.585938 C 39.523438 3.59375 39.511719 3.597656 39.503906 3.605469 L 4.300781 38.804688 C 4.179688 38.929688 4.089844 39.082031 4.042969 39.253906 L 2.035156 46.742188 C 1.941406 47.085938 2.039063 47.453125 2.292969 47.707031 C 2.484375 47.898438 2.738281 48 3 48 C 3.085938 48 3.171875 47.988281 3.257813 47.964844 L 10.746094 45.957031 C 10.917969 45.910156 11.070313 45.820313 11.195313 45.695313 L 46.394531 10.5 C 46.40625 10.488281 46.410156 10.472656 46.417969 10.460938 C 46.507813 10.371094 46.570313 10.308594 46.570313 10.308594 C 48.476563 8.40625 48.476563 5.324219 46.574219 3.425781 Z M 45.160156 4.839844 C 46.277344 5.957031 46.277344 7.777344 45.160156 8.894531 C 44.828125 9.222656 44.546875 9.507813 44.304688 9.75 L 40.25 5.695313 C 40.710938 5.234375 41.105469 4.839844 41.105469 4.839844 C 41.644531 4.296875 42.367188 4 43.132813 4 C 43.898438 4 44.617188 4.300781 45.160156 4.839844 Z M 5.605469 41.152344 L 8.847656 44.394531 L 4.414063 45.585938 Z"
                  ></path>
                </svg>
                <span class="text-white text-md">Edit</span>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div>
      <edit-todo :work="work" @save="clickSave" v-if="isEdit"></edit-todo>
    </div>
    <home-header></home-header>
   
    
  </id>

</template>

<script>

import EditTodo from "./components/EditTodo.vue";
import HomeHeader from "./components/HomeHeader.vue";
export default {
  name: "App",
  data() {
    return {
      todoL: [
        {
          id: 1,
          workName: "Hello", 
          completed: false
        },
        {
          id: 2,
          workName: "Todo",
        },
        {
          id: 3,
          workName: "Test",
        },
      ],
      work: null,
      isEdit: false,
    };
  },

  methods: {
    removeTodo(itemId) {
      this.todoL = this.todoL.filter((item) => item.id !== itemId);
    },
    clickAdd() {
      let work = {
        id: Math.floor(Math.random() * 10000),
        workName: "",
      };
      this.work = work;
      this.isEdit = true;
    },
    clickSave(work) {
      let index = this.todoL.findIndex((item) => item.id == work.id);
      if (index >= 0) {
        this.todoL.splice(index, 1, work);
      } else {
        this.todoL.push(work);
      }
      this.isEdit = false;
    },
    clickEdit(work) {
      this.work = work;
      this.isEdit = true;
    },
  },
  components: {
    "edit-todo": EditTodo,
    "home-header":HomeHeader
  },
};
</script>

<style>
.col-2 {
  text-align: center;
  font-weight: bold;
  font-size: 20px;
  color: blue;
}
.row {
  margin-top: 25px;
  margin-bottom: 20px;
  align-items: center;
}
.todo-list {
  margin: 0 100px 0 64px;
}
.table table-bordered thead th {
  border-bottom: none !important;
}
.action-td {
  text-align: center;
}
.action-td .btn-warning {
  margin-right: 10px;
}

</style>
<style src="./assets/tailwind.css"></style>
