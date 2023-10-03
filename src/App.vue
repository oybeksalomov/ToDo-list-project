<template>
  <div class="todoListBox">

    <div class="todoListTitleBox">
      <h1 class="todoListTitle">Loyiha nomi</h1>
    </div>

    <div class="todoList">
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
    </div>

    

    <button class="todoListAddBtn">Vazifa qo'shish</button>

  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  },
  data() {
    return {
      todoList: [
        {
          id: 1,
          body: "Uyga vazifalarni bajarish",
          isDone: false
        },
        {
          id: 2,
          body: "Yugurishga chiqish",
          isDone: false
        }
      ]
    }
  },
  methods: {
    toggleIsDone(taskId) {
      this.todoList.forEach(task => {
        if(task.id === taskId) {
          task.isDone = !task.isDone

        }
      })
    },
    deleteTask(taskId) {
      this.todoList = this.todoList.filter(task => task.id !== taskId)
    }
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

</style>
