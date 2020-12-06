<template>
  <div class="main">
      <div class="contact-form">
          <p class="contact-form__title"> Адрес </p>
          <input 
            type="text"
            id="index" 
            placeholder="Индекс" 
            class="contact-form__element"
            v-model="form.index"
          >

          <input 
            type="text" 
            v-model="form.country" 
            id="country" 
            placeholder="Страна" 
            class="contact-form__element"
          >

          <input 
            type="text" 
            v-model="form.region" 
            id="region" 
            placeholder="Область"  
            class="contact-form__element"
          >

          <input 
            type="text" 
            v-model="form.city" 
            id="city" 
            :class="{ 'form-group--error': $v.form.city.$error }" 
            placeholder="Город" 
            class="contact-form__element"
          >
          <div class="error" v-if="!$v.form.city.required && $v.form.city.$dirty">Это поле обязательно</div>

        <input 
            type="text" 
            v-model="form.street" 
            id="street" 
            placeholder="Улица" 
            class="contact-form__element"
          >
        <input 
            type="text" 
            v-model="form.house" 
            id="number" 
            placeholder="Дом" 
            class="contact-form__element"
          >
          <button type="submit" class="contact-form__btn" @click="showThirdForm">Создать</button>
      </div>
    </div>
</template>

<script>
import { required} from 'vuelidate/lib/validators'
export default {
  data() {
    return {
      form: {
        region: "",
        city: "",
        street: "",
        house: "",
        index: "",
        country: "",
      },
      secondFormShow: false
    }
  },
  methods: {
    handleSubmit() {
      console.log('submit!')
      this.$v.$touch()
      if (this.$v.$invalid) {
        this.submitStatus = 'ERROR'
        console.log('error')
      } else {
        this.submitStatus = 'PENDING'
      }
    },
    showThirdForm() {
      this.secondFormShow = false
    }
  },
  validations: {
    form: {
      city: {
        required
      }
    },
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input {
  outline: 0;
  border-width: 0 0 2px;
  border-color: grey;
  
}
input:focus {
  border-color: green;
}
.contact-form {
  margin: 40px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px 15px;
  width: 30%;
  border-radius: 10px;
  background-color: white;
  &__title {
    font-size: 1.5rem;
  }
  &__element {
    padding: 10px;
    margin: 10px;
    width: 90%;
  }
  &__btn {
    width: 50%;
    margin: 10px auto;
    padding: 10px;
    cursor: pointer;
  }
  &__row {

  display: block;
  margin-top: 0.5em;
  margin-bottom: 0.5em;
  margin-left: auto;
  margin-right: auto;
  border-style: inset;
  border-width: 1px;

  }
}
.main {
  
  display: flex;
  justify-content: center;
}
.error {
  color: red;
  margin: 0 auto;
  font-size: 0.75rem;
}
.form-group--error{
  outline: 0;
  border-width: 0 0 2px;
  border-color: red;
}
.not-text {
  padding-left: 5px;
}

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
