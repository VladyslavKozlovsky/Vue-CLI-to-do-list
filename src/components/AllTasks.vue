<template>
  <CreateTask v-on:add-task="createNewTask" v-on:delete-task="deleteAllTasks"/>
  <div class="all_tasks">
    <div v-for="task in state.active_tasks" :key="task.id" class="active_tasks">
      <span class="void"></span>
      <span class="act-move move icon-circle"></span>
      <span @click="move(task.text, task.id)" @mouseover="onHover" @mouseleave="onLeave" class="act-move move icon-caret-circle-down hidden"></span>
      <span class="act-text">{{ task.text }}</span>
      <span @click="deleteTask(task.id)" class="act-del del icon-eraser"></span>
    </div>
    <div v-for="com_task in state.completed_tasks" :key="com_task.id" class="completed_tasks">
      <span class="void"></span>
      <span class="com-move move icon-Check-circle"></span>
      <span @click="moveBack(com_task.text, com_task.id)" @mouseover="onHover" @mouseleave="onLeave" class="com-move move icon-caret-circle-up hidden"></span>
      <span class="com-text">{{ com_task.text }}</span>
      <span @click="deleteComTask(com_task.id)" class="com_del del icon-eraser"></span>
    </div>
  </div>


</template>

<script>
import CreateTask from './CreateTask';
import {reactive} from 'vue';

export default {
  name: 'AllTasks',
  components: { CreateTask },
  setup() {
    const state = reactive({
      active_tasks: [],
      completed_tasks: [],
      id: 0
    });

  function deleteTask(id) {
      let newAct_Arr = [];
      state.active_tasks.forEach(item => {
        if(item.id != id)
          newAct_Arr.push(item);
      });
      state.active_tasks = newAct_Arr;
  }

  function deleteComTask(id) {
    let newCom_Arr = [];
    state.completed_tasks.forEach(item => {
      if(item.id != id)
        newCom_Arr.push(item);
    });
    state.completed_tasks = newCom_Arr;
  }

  function createNewTask(newText) {
    let newText_true = newText.trim();
      if (newText_true) {
        state.id++;
        state.active_tasks.unshift({
          id: state.id,
          text: newText_true
        })
      }
  }

  function move(task, i) {
    state.completed_tasks.unshift({
      id: i,
      text: task,
    });
    deleteTask(i)
  }

  function moveBack(task, j) {
    state.active_tasks.unshift({
      id: j,
      text: task,
    });
    deleteComTask(j)
  }

  function deleteAllTasks() {
    state.active_tasks = [];
    state.completed_tasks = [];
    state.id = 0;
  }

  function onHover(event) {
    event.target.style.opacity = 1
  }

  function onLeave(event) {
    event.target.style.opacity = 0
  }

  return {
    state,
    createNewTask,
    deleteTask,
    deleteComTask,
    deleteAllTasks,
    move,
    moveBack,
    onHover,
    onLeave
    }
  }
}

</script>

<style>
.all_tasks {
  margin-top: 20px;
  height: 415px;
  overflow: auto
}

.all_tasks::-webkit-scrollbar {
    width: 10px;
    background-color: #010510;
}

.all_tasks::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background-color: #4676dc
}

.active_tasks, .completed_tasks {
  position: relative;
  margin: 10px 0;
}

.act-text, .com-text {
  display: inline-block;
  width: 260px;
  word-wrap: break-word;
  margin-left: 30px;
}

.com-text {
  color: #7a7a7a
}

.del {
  float: right;
  margin-right: 20px;
}

.act-move, .act-del {color: #4676dc}

.com-move, .com_del {color: #1f3563}

.act-move, .act-del, .com-move, .com_del, .void {
  display: inline-block;
  height: 25px;
  font-size: 28px;
  padding: 0 10px 0 20px;
  cursor: pointer;
}

.act-move, .com-move, .hidden {
  position: absolute;
  top: 0;
  left: 0;
}

.hidden {
  opacity: 0;
  background: #010510;
  color: #fafafa;
  text-shadow:0 0 20px #4676dc;
}

.act-del, .com_del {position: absolute;}

.act-del:hover, .com_del:hover {
  color: #fafafa;
  text-shadow:0 0 20px #4676dc
}

</style>
