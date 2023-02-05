<template>
  <div class="container-fluid">
    <div class="home d-flex justify-content-center row pt-3 pb-3">
      <div class="col-md-4 mb-2">
        <TaskForm/>
      </div>
      <div class="col-md-8 mb-2" id="list">
        <TaskList/>
      </div>
    </div>
  </div>
</template>

<script>
import TaskForm from '@/components/TaskForm.vue';
import TaskList from '@/components/TaskList.vue';

export default {
  name: 'HomeView',
  components: {
    TaskList,
    TaskForm
  }
}
</script>

<style>
.home{
  background: url('https://www.showmetech.com.br/wp-content/uploads//2022/01/3585739-1920x1024.jpg') var(--cor-primaria) no-repeat;
    background-size: cover;
    background-blend-mode: overlay;
    min-height: calc(100vh - 84px)
}
#list{
  overflow: auto;
  scrollbar-width: 60px;
  height: 80vh;
}

@media only screen and (max-width: 764px) {
  #list{
    margin-left:30px;
  }
}

@media only screen and (max-width: 717px) {
  #list{
    margin-left:10px;
  }
}
</style>
