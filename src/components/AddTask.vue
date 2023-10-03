<template>
  <div class="addTaskBox" v-if="isShow === true">
    <div class="addTaskContent">
      <h2 class="addTaskTitle">Vazifa qo'shish</h2>
      <form @click.prevent>
        <input type="text" class="addTaskInput" v-model="task.body">
        <div class="addTaskBtnBox">
          <button class="addTaskBtn" @click="closeModal">Bekor qilish</button>
          <button class="addTaskBtn" @click="createTask">Qo'shish</button>
        </div>
      </form>
    </div>

  </div>
</template>

<script>
  export default {
    name: 'addTask',
    data() {
      return {
        task: {
          body: '',
          isDone: false
        }
      }
    },
    props: {
      isShow: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      closeModal() {
        this.$emit('update:isShow', false)
      },
      createTask() {
        this.task.id = Date.now()
        this.$emit('create', this.task)
        this.task = {
          body: '',
          isDone: false
        }
      }
    }
  }
</script>

<style scoped>
  .addTaskBox {
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background: rgb(0,0,0, 0.5);
    position: fixed;
    display: flex;
  }
  .addTaskContent {
    margin: auto;
    background: #fff;
    min-height: 50px;
    width: 100%;
    max-width: 400px;
    padding: 30px;
  }
  .addTaskTitle {
    text-align: center;
    margin-bottom: 25px;
    color: #9A9DA7;
  }
  .addTaskInput {
    color: #9A9DA7;
    padding: 10px;
    font-size: 18px;
    width: 100%;
    border-color: #00000049;
    margin-bottom: 25px;
  }
  .addTaskBtnBox {
    display: flex;
    justify-content: space-between;
  }

  .addTaskBtn {
    padding: 15px 25px;
    font-weight: 700;
    font-size: 20px;
    background-color: #A879E2;
    color: #fff;
    border: none;
    display: flex;
    cursor: pointer;
    justify-content: center;
  }
</style>