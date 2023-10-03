<template>
  
  <div class="todoListBox">

    <div class="todoListTitleBox">
      <input type="text" class="titleInput" v-model="projectTitle" >
    </div>

    <div class="todoList">
      <TransitionGroup name="todoList">
        <div 
          class="todoItem"
          v-for="item of todoList" 
          :key="item.id"
        >
          <button class="tosoListCheckBtn" @click="toggleIsDone(item.id)">
            <i class="fa-regular fa-circle-check fa-xl" v-if="item.isDone"></i>
            <i class="fa-regular fa-circle fa-xl" v-else></i>
          </button>
          <p :class="item.isDone ? 'throughLine' : ''">{{ item.body }}</p>
          <button class="todoListBtn" @click="deleteTask(item.id)"><i class="fa-regular fa-trash-can fa-xl"></i></button>
        </div>
      </TransitionGroup>

    </div>

    <button class="todoListAddBtn" @click="openModal">Vazifa qo'shish</button>

  </div>
  <AddTask 
    v-model:isShow="isVisible" 
    @create="createTask"
  ></AddTask>
</template>

<script>
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    AddTask
  },
  data() {
    return {
      todoList: [],
      isVisible: false,
      projectTitle: 'Loyiha Nomi' ,
    }
  },
  methods: {
    toggleIsDone(taskId) {
      let existingArray = JSON.parse(localStorage.getItem('todoList'))
      existingArray.forEach(task => {
        if(task.id === taskId) {
          task.isDone = !task.isDone

        }
      })
      localStorage.setItem('todoList', JSON.stringify(existingArray))

      this.todoList = JSON.parse(localStorage.getItem('todoList'))
    },
    deleteTask(taskId) {
      this.todoList = this.todoList.filter(task => task.id !== taskId)

      let existingArray = JSON.parse(localStorage.getItem('todoList'))
      let filteredArr = existingArray.filter(task => task.id !== taskId)
      localStorage.setItem('todoList', JSON.stringify(filteredArr))

      this.todoList = JSON.parse(localStorage.getItem('todoList'))
    },
    openModal() {
      this.isVisible = true
    },
    createTask(task) {
      let existingArray = JSON.parse(localStorage.getItem('todoList'))
      existingArray.push(task)
      localStorage.setItem('todoList', JSON.stringify(existingArray))

      this.todoList = JSON.parse(localStorage.getItem('todoList'))

      this.isVisible = false
    }
  },
  watch: {
    projectTitle(newValue) {
      localStorage.setItem('projectTitle', newValue)
      document.title = localStorage.getItem('projectTitle')
    }
  },
  mounted() {
    if(!JSON.parse(localStorage.getItem('todoList'))) {
      localStorage.setItem('todoList', JSON.stringify([]))
    }
    this.todoList = JSON.parse(localStorage.getItem('todoList'))
    document.title = this.projectTitle
    this.projectTitle = localStorage.getItem('projectTitle') || 'Loyiha Nomi'
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: sans-serif;
  background-color: #DAE0F5;

}
#app {
  width: 100%;
  padding-top: 100px;
}
.todoListBox {
  width: 100%;
  max-width: 600px;
  margin: auto;
}
.todoListTitleBox {
  padding: 20px;
  text-align: center;
  background-color: #A879E2;
}
.todoListTitle {
  color: #fff;
}
.todoList {
  width: 100%;
  padding: 50px 30px;
  margin-top: 30px;
  background-color: #F5F5F5;
  
}
.titleInput {
  background: transparent;
  border: none;
  text-align: center;
  color: #fff;
  font-size: 24px;
  font-weight: 700;
}
.titleInput:focus {
  outline: none;
  border: none;
}
.todoItem {
  width: 100%;
  display: flex;
  justify-content: space-between;
  margin-bottom: 30px;
}
.todoItem:last-child {
  margin: 0;
}
.todoItem p {
  color: #9A9DA7;
  padding: 0 10px;
  font-size: 18px;
  width: 100%;
}
.throughLine {
  text-decoration: line-through;
}
.todoItem button {
  background-color:#ffffff00;
  border: none;
  cursor: pointer;
}
.todoItem button i{
  color: #9A9DA7;
}
.todoListAddBtn {
  padding: 15px 25px;
  font-weight: 700;
  font-size: 20px;
  background-color: #A879E2;
  color: #fff;
  border: none;
  transform: translateY(-50%);
  margin: auto;
  display: flex;
  border-radius: 25px;
  cursor: pointer;
}
.todoList-enter-active,
.todoList-leave-active {
  transition: opacity 0.5s ease;
}

.todoList-enter-from,
.todoList-leave-to {
  opacity: 0;
}
</style>
