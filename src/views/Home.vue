<template>
  <div class="home">
    <header>
      <div><img alt="Vue logo" src="../assets/logo.png"></div>
      <div>
        <input type="search" placeholder="Pesquisar endereço">
      </div>
      <div class="user">
          <strong>{{this.user.name}}</strong>
          <small>{{this.user.access}}</small>
        </div>
      <div>
        <button v-on:click="logout()">Sair</button>
      </div>
    </header>
    <main>
      <div>
        <form v-on:submit.prevent="Add()">
          <span>
            <h4>Atalho p/ adicionar endereço</h4>
          </span>
          <span>
            <label for="long_name">Designação</label>
          <input type="text" id="long_name" placeholder="nome longo" v-model="long_name" required>
          </span>
          <span>
            <label for="short_name">Simplificado</label>
          <input type="text" id="short_name" placeholder="nome curto" v-model="short_name" required>
          </span>
         <span>
            <label for="lat">Latitude</label>
          <input type="number" id="lat" placeholder="-415323.5" v-model="lat" required>
          </span>
          <span>
            <label for="lng">Longitude</label>
          <input type="number" id="lng" placeholder="865412.24" v-model="lng" required>
          </span>
        <div>
          <div/>
           <div>
             <button type="submit">Adicionar</button>
           </div>
        </div>
        </form>
      </div>
      <div class="tableConatiner">
      <table >
        <thead>
          <tr>
            <th>id</th>
            <th>Designação</th>
            <th>Simplificado</th>
            <th>Latitude</th>
            <th>Longitude</th>
          </tr>
        </thead>
        <tbody v-for="(address, index) in addresses" v-bind:key="{index}">
          <tr>
            <td>{{address?.id}}</td>
            <td>{{address?.long_name}}</td>
            <td>{{address?.short_name}}</td>
            <td>{{address?.lat}}</td>
            <td>{{address?.lng}}</td>
          </tr>
        </tbody>
      </table>
      </div>
    </main>
  </div>
</template>

<script>
import Api from '../api'

export default {
  name: 'Home',
  data: ()=>{
    return {
      addresses: [],
      long_name: '',
      short_name: '',
      lat: '',
      lng: '',
      user:{
        name: 'Tets',
        access: 'asd'
      }
    }
  },
  methods: {
   Add(){
      Api.post('/address',{
        long_name: this.long_name,
      short_name: this.short_name,
      lat: this.lat,
      lng: this.lng
      })
      .then(({ data })=>{
        if(data?.result)alert('Salvo!')
      })
      .catch(error=>alert(error))
    },
    logout(){
      sessionStorage.removeItem('lrinfo')
      location.href = '/'

      Api.post(`/logOut/${this.user?.token}`)
    }
  },
   mounted() {
      Api.get("/address")
        .then(response => {
          this.addresses = response.data
          const data = JSON.parse(sessionStorage.getItem('lrinfo'))

          this.user = {...data?.user, token: data?.token}
        });
    }
}
</script>
<style>
  .home{
    flex: 1;
    display: flex;
    flex-direction: column;
    height: 100%;
  }
  header{
    background-color: #fff;
    display: flex;
    flex-direction: row;
    border-bottom: solid 1px #ddd;
    padding: 1rem 2rem;
  }
  .user{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-right: 1rem;
  }
  header>div:nth-child(2){
    flex: 1;
  }
  header img{
    width: 2rem;
  }
  main{
    display: flex;
    flex: 1;
    flex-direction: row;
    padding: 2rem;
  }
  form{
  display: flex;
  flex-direction: column;
  padding: 1rem;
  border-radius: 4px;
  background-color: #fff;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.1);
  margin-right: 2rem;
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
.tableConatiner{
  width: 100% !important;
}
.tableConatiner table {
  width: 100% !important;
}

.tableConatiner th {
  font-size: 10pt;
  text-transform: uppercase;
  font-weight: normal;
  color: rgba(0, 0, 0, 0.5);
}

.tableConatiner th,
.tableConatiner td {
  text-align: center;
  padding: 1rem;
  cursor: default;
}

.tableConatiner tr {
  -webkit-transition: all 0.2s;
  transition: all 0.2s;
}

.tableConatiner tbody tr:hover {
  background-color: rgba(0, 0, 0, 0.06);
}

.tableConatiner tbody tr:not(:last-child) {
  border-bottom: solid 1px rgba(0, 0, 0, 0.06);
}
</style>