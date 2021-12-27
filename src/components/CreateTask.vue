<template>
  <div class="form">
    <form @submit.prevent="createNewTask">
      <div class="logo"><h1>Список дел</h1></div>
      <div class="new-task">
        <input type="text" class="input" v-model="state.newTask" placeholder="...">
        <button @click="createNewTask" class="add-btn btn icon-Pen-alt"></button>
      </div>
      <button @click="deleteAllTasks" class="del-btn btn icon-bomb"></button>
    </form>
  </div>
</template>

<script>
import {reactive} from 'vue';

export default {
  name: 'CreateTask',

  setup(props, ctx) {
    const state = reactive({
      newTask: '',
    });

    function createNewTask() {
      if(state.newTask) {
        ctx.emit('add-task', state.newTask);
        state.newTask = '';
      }
    }

    function deleteAllTasks() {
      ctx.emit('delete-task');
    }

    return {
      state,
      createNewTask,
      deleteAllTasks
    }
  }
}
</script>

<style>
* {outline: 0}

@font-face {
  font-family: 'icons';
  src:  url('../fonts/icons.eot?56gt57');
  src:  url('../fonts/icons.eot?56gt57#iefix') format('embedded-opentype'),
    url('../fonts/icons.ttf?56gt57') format('truetype'),
    url('../fonts/icons.woff?56gt57') format('woff'),
    url('../fonts/icons.svg?56gt57#icons') format('svg');
  font-weight: normal;
  font-style: normal;
  font-display: block;
}

[class^="icon-"], [class*=" icon-"] {
  font-family: 'icons' !important;
  speak: never;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;

  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-bomb:before {
  content: "\e900";
}
.icon-caret-circle-down:before {
  content: "\e901";
}
.icon-caret-circle-up:before {
  content: "\e902";
}
.icon-Check-circle:before {
  content: "\e903";
}
.icon-circle:before {
  content: "\e904";
}
.icon-eraser:before {
  content: "\e905";
}
.icon-Pen-alt:before {
  content: "\e906";
}

.form {position: relative}

.logo {
  text-align: center;
  color: #4676dc;
}

.logo h1 {
  padding: 10px;
  font-size: 24px;
}

.new-task {
  text-align: center;
  width: 100%;
  border-bottom: 2px solid #22324c
}

.input {
  padding: 10px;
  /* text-indent: 5px; */
  color: #e3e3e3;
  width: 75%;
}

.input::-webkit-input-placeholder { color: #4676dc }
.input::-moz-placeholder { color: #4676dc }

.input, .add-btn, .del-btn {
  border: 0;
  background: #010510;
  cursor: pointer;
}

.btn {
  color: #4676dc;
  display: inline-block;
}

.add-btn {
  width: 10%;
  padding: 10px;
  font-size: 24px;
}

.del-btn {
  position: absolute;
  font-size: 30px;
  top: 555px;
  left: 179px;
}

.add-btn:hover, .del-btn:hover {
  color: #fafafa;
  text-shadow:0 0 20px #4676dc
}
</style>
