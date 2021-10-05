<template>
  <div class="container">
    
        <form v-on:submit.prevent="In()">
          <span>
            <h4>Criar conta</h4>
          </span>
          <span>
            <label for="name">Nome</label>
          <input type="text" id="name" placeholder="Nome completo" v-model="name" required>
          </span>
          <span>
            <label for="email">Usuário</label>
          <input type="email" id="email" placeholder="Email" v-model="email" required>
          </span>
          <span>
            <label for="access">access</label>
            <select id="access" v-model="access" required>
              <optgroup>
                <option value="administrador">administrador</option>
                <option value="usuario">usuario</option>
              </optgroup>
            </select>
          </span>
          <span>
            <label for="password">Senha</label>
        <input type="password" id="password" v-model="password" required>
          </span>
        <div>
          <div/>
          <div style="margin: 0 .5rem;">
            <router-link to="/"><button type="submit" style="background-color: #ccc;">Cancelar</button></router-link>
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
        password: '',
        name: '',
        access: ''
      }
  },
  methods: {
    In(){
      Api.post('/register',{
        "email": this.email,
        "password": this.password,
        "name": this.name,
        "access": this.access
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
h4{
  color: var(--primary);
}
form{
  display: flex;
  flex-direction: column;
  padding: 1rem;
  border-radius: 4px;
  background-color: #fff;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.1);
}
form>*:not(:first-child){
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