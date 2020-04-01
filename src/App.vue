<template>
    <div id="app">
      
      <div class="jumbotron jumbotron-fluid">
        <div class="container">
          <h1 class="display-4">Animações</h1>
          <p class="lead">Transição/animação de elementos/componentes no Vue.</p>
        </div>
      </div>

      <div class="container">
        <!-- <button class="btn btn-primary mb-3" @click="mostrar = !mostrar">Alternar</button> -->

        <div class="form-group">
          <label>Animações:</label>
          <select class="form-control" v-model="alertaAtual">
            <option value="info">Informação</option>
            <option value="warning">Alerta</option>
            <option value="success">Sucesso</option>
          </select>
        </div>

        <div class="form-group">
          <label>Componente:</label>
          <select class="form-control" v-model="componenteSelecionado">
            <option value="AppHome">Home</option>
            <option value="AppSobre">Sobre</option>
          </select>
        </div>

        <transition :name="animacaoSelecionada" mode="out-in">
          <component :is="componenteSelecionado"></component>
        </transition>
      </div>

    </div>
</template>

<script>

export default {
  components: {
    AppHome: () => import('./components/Home.vue'),
    AppSobre: () => import('./components/Sobre.vue')
  },
  data(){
    return {
      mostrar: true,
      animacaoSelecionada: 'fade',
      alertaAtual: 'info',
      componenteSelecionado: 'AppHome'
    }
  },
  computed: {
    classeDeAlerta(){
      return {
        alert: true,
        [`alert-${this.alertaAtual}`] : true
      }
    }
  }
}
</script>

<style>
  body{
    overflow: hidden;
  }
</style>
<style scoped>
  .slide-enter, .slide-leave-to {
    opacity: 0;
  }
  .slide-enter-active {
    animation: slide 0.7s;
    transition: opacity 0.7s;
  }
  .slide-leave-active {
    animation: slide 0.7s reverse;
    transition: opacity 0.7s;
  }
  
  @keyframes slide {
    0% {
      transform: translateX(-100px);
    }
    100% {
      transform: translateX(0px);
    }
  }

  /* Zoom */
  .zoom-enter, .zoom-leave-to {
    transform: scale(0);
  }
  .zoom-enter-active, .zoom-leave-active {
    transition: transform 0.5s;
  } 

  /* Fade */
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
  .fade-enter-active, .fade-leave-active  {
    transition: opacity 1s;
  }

</style>