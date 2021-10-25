<template>
  <div class="feature-block">
    <h3>Daily routines</h3>
    <h4>{{ getRoutineDate(routineId) }}</h4>
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
    <div>
      <div>
        <button @click="resetRoutines">Reset</button>
      </div>
      <div>
        <label for="routines">Select a past record:</label>
        <select name="routines" id="routines" v-model="routineId">
          <option
            v-for="(routine, i) in dataList"
            :key="i"
            :value="Object.keys(routine)[0]"
            @change="selectCurrentRoutines(routine)"
          >
            {{ getRoutineDate(Object.keys(routine)[0]) }}
          </option>
        </select>
      </div>
    </div>
  </div>
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
        { name: "Meditate", id: 6, checked: false },
        { name: "Play", id: 7, checked: false },
      ],
      routineId: "",
      dataList: [],
      currentDate: "",
      trimedDate: "",
    }
  },
  created() {
    this.currentDate = new Date().toISOString()
    this.trimedDate = this.currentDate.slice(
      0,
      this.currentDate.lastIndexOf("T")
    )
    this.routineId = `routines-${this.trimedDate}`
    if (localStorage.getItem(this.routineId)) {
      this.routines = this.getRoutines(this.routineId)
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
      localStorage.setItem(this.routineId, JSON.stringify(this.defaultRoutines))
      this.routines = this.getRoutines(this.routineId)
    },
    getRoutines(id) {
      return JSON.parse(localStorage.getItem(id))
    },
    getAllRoutines() {
      const allKeyEntries = Object.keys(localStorage)
      return allKeyEntries
        .filter(e => e.includes("routines-"))
        .map(e => {
          return { [e]: JSON.parse(localStorage.getItem(e)) }
        })
    },
    selectCurrentRoutines(routine) {
      this.routines = this.getRoutines(Object.keys(routine)[0])
    },
    getRoutineDate(id) {
      return id.substring("routines-".length)
    },
  },
  watch: {
    routines: {
      handler() {
        localStorage.setItem(this.routineId, JSON.stringify(this.routines))
      },
      deep: true,
    },
    routineId: {
      handler() {
        this.routines = this.getRoutines(this.routineId)
      },
      deep: true,
    },
  },
}
</script>

<style scoped>
.feature-block {
  display: flex;
  flex-direction: column;
  border: 1px seagreen solid;
  padding-bottom: 8px;
  width: 25%;
}
</style>
