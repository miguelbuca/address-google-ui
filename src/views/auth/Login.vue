<template>
  <div class="container">
    <img alt="Vue logo" src="../../assets/logo.png">
        <form v-on:submit.prevent="In()">
          <span>
            <label for="email">Usuário</label>
          <input type="email" id="email" placeholder="Email" v-model="email" required>
          </span>
          <span>
            <label for="password">Senha</label>
        <input type="password" id="password" v-model="password" required>
          </span>
        <div>
          <div class="account">
            <label>You have account?</label> <small><router-link to="/register">Registar</router-link></small>
          </div>
           <div>
             <button type="submit">Login</button>
           </div>
        </div>
        </form>
  </div>
</template>

<script>

import Api from '../../api'

export default {
  name: 'Login',
  data:()=>{
      return {
        email: '',
        password: ''
      }
  },
  methods: {
    In(){
      Api.post('/login',{
        "email": this.email,
        "password": this.password
      })
      .then(({ data })=>{
        sessionStorage.setItem('lrinfo',JSON.stringify(data))
        window.location.href = '/home'
      })
      .catch(error=>alert(error))
    }
  }
}
</script>

<style scoped>
.container{
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background: linear-gradient(to bottom, #fff 50%, var(--sec) 50%) !important;
}
.container>img{
  max-width: 8rem;
  height: auto;
  margin-top: -10rem;
  margin-bottom: 5rem;
}
.account{
  display: flex;
  align-items: center;
}
.account>*:first-child{
  margin-right: .3rem;
}
form{
  display: flex;
  flex-direction: column;
  margin-top: -4rem;
  padding: 1rem;
  border-radius: 4px;
  background-color: #fff;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.1);
}
form>*{
  margin-top: 2rem;
}
form span{
  display: flex;
  flex-direction: column;
  text-align: start;
}
form span label{
  margin-bottom: .2rem;
}
.container>*:first-child{
  background-origin: red;
  padding-top: 2rem;
}
form>*:last-child{
  display: flex;
  flex-direction: row;
  margin-top: 2rem;
}
form>*:last-child>div:first-child{
  flex: 1;
}
form>*:last-child>div{
  display: flex;
  align-items: center;
}
</style>