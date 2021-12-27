<template>
  <div class="frame">
    <AllTasks />
  </div>
</template>

<script>
import AllTasks from './components/AllTasks'


export default {
  name: 'App',
  components: {
    AllTasks
  }
}
</script>

<style>
@font-face {
  font-family: "Jura";
  src: url("/fonts/Jura-Regular.ttf") format("truetype");
  font-style: normal;
  font-weight: normal;
}

* {font-size: 20px}

body {
  background: #4676dc;
  background: -moz-radial-gradient(circle, #4676dc 0%, #010510 100%);
  background: -webkit-radial-gradient(circle, #4676dc 0%, #010510 100%);
  background: radial-gradient(circle, #4676dc 0%, #010510 100%);
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#4676dc",endColorstr="#010510",GradientType=1);
}

.frame {
  width: 400px;
  height: 600px;
  border: 0;
  border-radius: 20px;
  margin: 50px auto;
  background: #010510;
  color: #e3e3e3;
  font-family: "Jura", sans-serif;
  box-shadow: 5px 3px 2px #010510aa;
}
</style>
