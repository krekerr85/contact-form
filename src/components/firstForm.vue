<template>
  <div class="main">
    <div class="contact-form">
          <p class="contact-form__title"> Заполните информацию о себе </p>
          <input 
            type="text"
            v-model.trim="$v.form.surName.$model" 
            id="surName" 
            placeholder="Фамилия" 
            :class="{ 'form-group--error': $v.form.surName.$error }" 
            class="contact-form__element"
          >
          <div class="error" v-if="!$v.form.surName.required && $v.form.surName.$dirty">Это поле обязательно</div>

          <input 
            type="text" 
            v-model="form.name" 
            id="name" 
            placeholder="Имя" 
            :class="{ 'form-group--error': $v.form.name.$error }" 
            class="contact-form__element"
          >
          <div class="error" v-if="!$v.form.name.required && $v.form.name.$dirty">Это поле обязательно</div>

          <input 
            type="text" 
            v-model="form.fatherName" 
            id="fatherName" 
            placeholder="Отчество"  
            class="contact-form__element"
          >

          <input 
            type="text" 
            v-model="form.birthday" 
            id="birthday" 
            :class="{ 'form-group--error': $v.form.birthday.$error }" 
            placeholder="Дата рождения" 
            class="contact-form__element"
          >
          <div class="error" v-if="!$v.form.birthday.required && $v.form.birthday.$dirty">Это поле обязательно</div>

          <input 
            type="text" 
            v-model.trim="$v.form.number.$model" 
            id="number" 
            placeholder="Номер телефона" 
            :class="{ 'form-group--error': $v.form.number.$error }" 
            class="contact-form__element"
          >
          <div class="error" v-if="!$v.form.number.numValidator && $v.form.number.$dirty">Некорректный номер телефона</div>

          <select name="sex" id="sex" v-model="form.sex" class="contact-form__element">
            <option selected value="" disabled>Пол</option>
            <option value="male">Мужчина</option>
            <option value="female">Женщина</option>
          </select>

          <select name="doctor" id="doctor" v-model="form.doctor" class="contact-form__element">
            <option selected value="" disabled>Врач</option>
            <option value="Ivanov">Иванов</option>
            <option value="Zaharov">Захаров</option>
            <option value="Chernisheva">Чернышева</option>
          </select>

          <div class="contact-form__element">
            <input type="checkbox" id="notification" v-model="form.notification"> <span class="not-text"> Не отправлять смс</span> 
          </div>
          <button type="button" class="contact-form__btn" @click="nextForm">Создать</button>
        </div>
      </div>
</template>

<script>
import { numValidator } from '../utils/validator'
import { required} from 'vuelidate/lib/validators'
export default {
  data() {
    return {
      form: {
        surName: "",
        name: "",
        fatherName: "",
        birthday: "",
        number: "",
        sex: "",
        clientGroup: [],
        doctor: "",
        notification: false
      },
      firstFormShow: true,
      secondFormShow: false
    }
  },
  methods: {
    nextForm() {
      console.log('submit!')
      this.$v.$touch()
      if (this.$v.$invalid) {
        console.log('error')
      } else {
        this.$emit('nextForm')
      }
    },
    showSecondForm() {
      this.firstFormShow = false
    }
  },
  validations: {
    form: {
      surName: {
      required
    },
      name: {
        required
      },
      fatherName: {
        required
      },
      birthday: {
        required
      },
      number: {
        numValidator,
      },
      sex: {
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


</style>
