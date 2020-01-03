<template>
    <tr>
        <td>{{ task.id }}</td>
        <td>{{ task.title }}</td>
        <td>{{ task.priority }}</td>
        <td><button @click="remove(task)" class="btn btn-danger">Remove</button></td>
    </tr>

</template>

<script>
  export default {
    props: {
      task: { type: Object }
    },
    data () {
      return {

      }
    },
    methods: {
      remove (task) {
        this.$emit('remove', task.id)
      }
    }
  }
</script>

<style>

</style>
