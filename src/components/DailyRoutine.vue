<template>
  <div id="list-rendering">
    <TodoItem
      v-for="(todo, i) in routines"
      :key="i"
      :id="todo.id"
      :name="todo.name"
      :checked="todo.checked"
      @updateTodoStatus="click"
    />
  </div>
  <!-- Add a select to get specific daily routines -->
  <button @click="resetRoutines">Reset</button>
</template>

<script>
import TodoItem from "./base/TodoItem.vue"
export default {
  components: {
    TodoItem,
  },
  props: {},
  data() {
    return {
      routines: [],
      defaultRoutines: [
        { name: "Health care", id: 0, checked: false },
        { name: "Draw", id: 1, checked: false },
        { name: "Music", id: 2, checked: false },
        { name: "Sport", id: 3, checked: false },
        { name: "Wood", id: 4, checked: false },
        { name: "Plants care", id: 5, checked: false },
      ],
      trimedDate: "",
      dataList: [],
    }
  },
  created() {
    const currentDate = new Date().toISOString()
    const trimedDate = currentDate.slice(0, currentDate.lastIndexOf("T"))
    this.trimedDate = `routines-${trimedDate}`
    if (localStorage.getItem(this.trimedDate)) {
      this.routines = this.getRoutines()
    } else {
      this.resetRoutines()
    }

    this.dataList = this.getAllRoutines()
  },
  methods: {
    click({ id, checked }) {
      this.routines[id].checked = !checked
    },
    resetRoutines() {
      localStorage.setItem(
        this.trimedDate,
        JSON.stringify(this.defaultRoutines)
      )
      this.routines = this.getRoutines()
    },
    getRoutines() {
      return JSON.parse(localStorage.getItem(this.trimedDate))
    },
    getAllRoutines() {
      const allKeyEntries = Object.keys(localStorage)
      return allKeyEntries
        .filter(e => e.includes("routines-"))
        .map(e => {
          return JSON.parse(localStorage.getItem(e))
        })
    },
  },
  watch: {
    routines: {
      handler() {
        localStorage.setItem(this.trimedDate, JSON.stringify(this.routines))
      },
      deep: true,
    },
  },
}
</script>
