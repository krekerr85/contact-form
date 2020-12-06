<template>
  <div>
    <form @submit.prevent="handleSubmit" class="contact-form">
        <transition name="slide-fade">
            <first-form v-if="show1" @nextForm="nextForm"/>
        </transition>
        <transition name="slide-fade">
            <second-form v-if="show2"/>
        </transition>
    </form>
  </div>
</template>

<script>
import firstForm from './firstForm.vue'
import secondForm from './secondForm.vue'

export default {
  name: 'App',
  components: {
    firstForm,
    secondForm
  },
  data(){
      return {
          show1: true,
          show2: false
      }
  },
  methods: {
      nextForm(){
        this.show1 = false;
        this.show2 = true
  },
      handleSubmit() {
          console.log('submitted')
      }
  }
  
}
</script>

<style>
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active до версии 2.1.8 */ {
  transform: translateX(-10px);
  opacity: 0;
}
</style>
