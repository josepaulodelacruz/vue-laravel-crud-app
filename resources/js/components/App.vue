<template>
    <div class="app-component" >

       <table class="table">
           <thead>
                <tr>
                    <th>id</th>
                    <th>Task Title</th>
                    <th>Priority</th>
                    <th>Action</th>
                </tr>
           </thead>
           <tbody>

           <tasks v-for="task in tasks" :key="task.id" :task="task" @remove="deleteTask"></tasks>
               <tr>
                   <td><input v-model="task.title" type="text" id="task" class="form-control"></td>
                   <td>
                       <select v-model="task.priority" id="select" class="form-control">
                           <option>Low</option>
                           <option>Medium</option>
                           <option>High</option>
                       </select>
                   </td>

                   <td><button @click="store" @keydoww.enter="store" class="btn btn-primary">ADD</button></td>
               </tr>
           </tbody>
       </table>


    </div>
</template>

<script>
import TaskComponent from './Task'
import axios from 'axios'
export default {
  components: {
    'tasks': TaskComponent
  },


  data () {
    return {
      tasks: [],
      task: { title: '', priority: 'Low' }
    }
  },


  methods: {
    getTask () {
      axios.get('/api/tasks')
          .then(({data}) => {
            data.map(task => {
              this.tasks.push(task)
            })
          })
          .catch(err => console.log(err))
    },
    store () {
      axios.post('/api/tasks', this.task).then(savedTask => {
        this.tasks.push(savedTask.data)
      })
          .catch(err => alert(err))


      console.log(this.task.priority)

      this.task = {
        title: '',
        priority: 'Low'
      }
    },
    deleteTask (id) {
      axios.delete(`/api/tasks/${id}`).then(() => {
        this.tasks = this.tasks.filter(x => x.id !== id)
      })
      console.log(id)
    }
  },


  created () {
    this.getTask()
  },
}
</script>

<style>

</style>
