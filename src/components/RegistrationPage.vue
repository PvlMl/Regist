<template>
  <div class="form-wrap">
    <div class="form-text">
      <h1>Регистрация</h1>
      <p>В качестве кого регистрируетесь?</p>
      <button :class="{'blue-button': selectedServiceType === 'customer'}"
      @click="selectedServiceType = 'customer'"
      >Заказчик</button>
      <button :class="{'blue-button': selectedServiceType === 'freelancer'}"
      @click="selectedServiceType = 'freelancer'"
      >Исполнитель</button>
    </div>
    <form class="register-form" @submit.prevent="sendDataRegist">
      <label>Имя</label><br />
      <input type="text" name="name"/>
      <label>Номер телефона</label><br />
      <input type="tel" name="phone"/>
      <label>E-mail</label><br />
      <input type="email" name="email"/>
      <label>Как узнали про нас</label><br />
      <input type="text" name="referral"/>
      <label>Пароль</label><br />
      <input type="password" name="password"/>
      <button class="blue-button">Зарегистрироваться</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data(){
    return{
      selectedServiceType: null
    }
  },
  methods: {
 async sendDataRegist(e){
    const inputs = new FormData(e.target);
   const data =  Object.fromEntries(inputs.entries());
   const sendData = {type: this.selectedServiceType, ...data};
     await axios({
  method: 'post',
  url: 'https://api.worldofjob.ru:3000/auth/register',
  data: sendData
});
    }
  }
};
</script>

<style lang="scss" scoped>
$primary-color: rgb(25,72,154);
$hover-color: rgb(15, 43, 90);
.form-wrap {
  width: 360px;
  margin: 3% auto;
}
.form-text{
  text-align: center;
  button{
    width: 155px;
    height: 50px;
    border-radius: 8px;
    border: none;
  }
}
.register-form {
  margin-top: 25px;
  input, button{
  width: 80%;
  display: block;
  margin: 25px auto;
}
button{
  height: 50px;
  border-radius: 25px;
}
input{
    font-size: 35px;
    background-color: rgb(248, 247, 247);
    border-radius: 8px;
    outline: none;
    border: none;
    margin-top: 0px;
  }
}
h1 {
  font-family: Arial, Helvetica, sans-serif;
}
label{
  margin-left: 32px;
}
.blue-button{
background: $primary-color;
color: white;
 &:hover{
   background: $hover-color;
 }
}
</style>

