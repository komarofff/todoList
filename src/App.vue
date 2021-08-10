<template>
  <div class="container">
    <div class="row mt-4">
      <div class="col6">
        <form class="form-group " @submit.prevent="addTask(new_task)" ref="form_1">
          <input class="form-control" :class="{'is-invalid': invalid}" type="text" v-model="new_task">
          <div class="invalid-feedback">
            Поле не может быть пустым
          </div>
          <button class="btn btn-success mt-2">Add new task</button>

        </form>
      </div>
    </div>
    <div class="row mt-4">
      <div class="col6">

        <ul class="list-group">
          <li class="list-group-item d-flex justify-content-between align-items-center" v-for="(item,index) in taskList"
              :class="{'dis': item.completed}" :key="item.id">
            {{ index + 1 }} ) {{ item.task }}
            <p class="d-flex justify-content-between align-items-center">
              <span><input type="checkbox" class="form-check-input mx-4"
                           @change="item.completed = !item.completed"></span>
              <button class="btn btn-danger" @click="deleteItem(index)">
                <span class="material-icons" >delete_forever</span>
              </button>
            </p>
          </li>
        </ul>

      </div>
    </div>

  </div>

</template>

<script>
export default {

  data() {
    return {
      invalid: false,
      new_task: null,
      newarr: [],
      taskList: [
        {id:1 , task: 'Установить Vue глобально', completed: false},
        {id:2 , task: 'Создать новый проект', completed: false},
        {id:3 , task: 'Подключить bootstrap5', completed: false},
        {id:4 , task: 'Создать скрипт todo (интерактивный список дел)', completed: false},
      ]
    }
  },
  computed:{
    getId(){
      return this.taskList.length+1
    }
  },
  methods: {
    addTask(new_task,) {
      if (new_task != null) {
        this.taskList.push({id: this.getId,task: new_task, completed: false})
        // this.newarr = this.taskList
        // console.log(this.newarr)
        this.invalid = false
        this.new_task = null
      } else {
        this.invalid = !this.invalid
      }
    },
    deleteItem(index) {
      this.taskList.splice(index, 1)
      console.log(this.taskList)
      // this.taskList[index].completed = false
    }
  }
}
</script>

<style>
.dis {
  color: #ccc;
  text-decoration: line-through;
}

.form-check-input:checked {
  background-color: #e9ecef;
  border-color: #e9ecef;
}
</style>
