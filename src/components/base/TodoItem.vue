<template>
  <div>
    <input
      class="todo-item"
      type="checkbox"
      :id="id"
      :name="name"
      :checked="checked"
      @click="$emit('updateTodoStatus', { id, name, checked })"
    />
    <label :for="id"> {{ name }}</label>
  </div>
</template>

<script>
export default {
  components: {},
  props: {
    id: Number,
    name: String,
    checked: Boolean,
  },
  emits: ["updateTodoStatus"],
}
</script>
