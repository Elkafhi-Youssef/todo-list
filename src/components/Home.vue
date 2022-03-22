<template>
  <div class="">
    <h1 class="text-center pt-4 text-3xl font-bold">My to do app</h1>
    <div id="input" class="flex mt-5 justify-center">
      <input
        v-model="task"
        type="text"
        class="
          form-control
          block
          w-6/12
          px-3
          py-1.5
          text-base
          font-normal
          text-gray-700
          bg-white bg-clip-padding
          border border-solid border-gray-300
          rounded-l
          transition
          ease-in-out
          m-0
          focus:text-gray-700
          focus:bg-white
          focus:border-blue-600
          focus:outline-none
        "
        id=""
        placeholder="Enter your tasck"
      />
      <button
        @click="addTasck"
        class="border-solid rounded-r bg-orange-500 px-2"
        type="submit"
      >
        Add
      </button>
    </div>
    <!-- <div
      class="
        flex flex-col
        justify-center
        mx-auto
        w-4/6
        mt-4
        border border-2 border-zinc-900
        p-7
      "
    >
      <div
        class="
          flex
          justify-between
          items-center
          mt-2
          px-3
          border border-2 border-zinc-50
        "
        v-for="(el, index) in tasks"
        :key="index"
      >
        <p>
          {{ el.task }}
        </p>
        <div>
          <button
            class="bg-red-500 rounded px-1 m-2"
            @click="updateTask(index)"
          >
            update
          </button>
          <button
            class="bg-red-500 rounded px-1 m-2"
            @click="deleteTask(index)"
          >
            delete
          </button>
        </div>
      </div>
    </div> -->
    <div class="flex flex-col justify-center w-3/4 mx-auto">
      <div class="overflow-x-auto mx-auto sm:-mx-6 lg:-mx-8">
        <div class="py-2 inline-block min-w-full sm:px-6 lg:px-8">
          <div class="overflow-hidden">
            <table class="min-w-full">
              <thead class="border-b">
                <tr>
                  <th
                    scope="col"
                    class="
                      text-sm
                      font-medium
                      w-3/5
                      text-gray-900
                      px-6
                      py-4
                      text-left
                    "
                  >
                    Tasks
                  </th>
                  <th
                    scope="col"
                    class="
                      text-sm
                      font-medium
                      w-1/5
                      text-gray-900
                      px-6
                      py-4
                      text-left
                    "
                  >
                    status
                  </th>
                  <th
                    scope="col"
                    class="
                      text-sm
                      font-medium
                      text-gray-900
                      px-6
                      py-4
                      text-left
                    "
                  >
                    #
                  </th>
                  <th
                    scope="col"
                    class="
                      text-sm
                      font-medium
                      text-gray-900
                      px-6
                      py-4
                      text-left
                    "
                  >
                    #
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr class="border-b" v-for="(el, index) in tasks" :key="index">
                  <td
                    class="
                      px-6
                      py-4
                      whitespace-nowrap
                      text-sm
                      font-medium
                      text-gray-900
                    "
                  >
                    <span
                      :class="{ finished: tasks[index].status == 'finished' }"
                    >
                      {{ el.task }}
                    </span>
                  </td>
                  <td
                    class="
                      text-xl
                      font-black
                      w-16
                      text-gray-900
                      px-6
                      py-4
                      whitespace-nowrap
                      cursor-pointer
                    "
                  >
                    <span
                      :class="{
                        'text-orange-500': el.status == 'to do',
                        ' text-amber-400': el.status == 'in-proccess',
                        ' text-green-600': el.status == 'finished',
                      }"
                      @click="changeStatus(index)"
                    >
                      <!-- {{upperFist(el.status)}} -->
                      {{ el.status }}
                    </span>
                  </td>
                  <td
                    class="
                      text-sm text-gray-900
                      font-light
                      px-6
                      py-4
                      whitespace-nowrap
                    "
                  >
                    <button
                      class="bg-green-500 rounded px-2 py-2 m-2"
                      @click="updateTask(index)"
                    >
                      update
                    </button>
                  </td>
                  <td
                    class="
                      text-sm text-gray-900
                      font-light
                      px-6
                      py-4
                      whitespace-nowrap
                    "
                  >
                    <button
                      class="bg-red-500 rounded px-2 py-2 m-2"
                      @click="deleteTask(index)"
                    >
                      delete
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home-com",
  data() {
    return {
      status: ["to do", "in-proccess", "finished"],
      editTask: null,
      task: "",
      tasks: [
        {
          task: "Create a simple page with router using Vuejs",
          status: "to do",
        },
      ],
    };
  },
  methods: {
    addTasck() {
      if (this.editTask === null) {
        this.tasks.push({ task: this.task, status: this.status[0] });
        this.task = "";
      } else {
        this.tasks[this.editTask].task = this.task;
        this.editTask = null;
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    updateTask(index) {
      this.task = this.tasks[index].task;
      this.editTask = index;
    },
    changeStatus(index) {
      let newIndex = this.status.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.status[newIndex];
    },
    // upperFist(str){
    //   return (str.charAt(0).toUpperCase() + str.splice(1))
    // }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.finished {
  text-decoration: line-through;
}
</style>
