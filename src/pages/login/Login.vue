<template>

  <login-template>
    <span slot="menuesquerdo">
      <img src="https://www.designerd.com.br/wp-content/uploads/2013/06/criar-rede-social.png" class="responsive-img">
    </span>
    <span slot="principal">
      <h2>Login</h2>
      <input type="text" placeholder="E-mail" v-model="email">
      <input type="password" placeholder="Senha" v-model="password">
      <button class="btn" v-on:click="login()">Entrar</button>
      <router-link to="/cadastro" class="btn orange">Cadastre-se</router-link>
    </span>
  </login-template>


</template>

<script>

import axios from 'axios';
import LoginTemplate from '@/templates/LoginTemplate';

export default {
  name: 'Login',
  data () {
    return {
      email:'',
      password:'',
    }
  },
  components:{
    LoginTemplate,
  },

  methods:{
    login(){      
      console.log(this.$urlApi+'login')
      return this.$http.post(this.$urlApi+'login', {
        email: this.email,
        password: this.password,
      })
      .then(response => {
        console.log(response)
        if (response.data.status) {
          //login com sucesso          
          sessionStorage.setItem('usuario', JSON.stringify(response.data.usuario))
          this.$router.push('/')
        }else if(response.data.status == false && response.data.validacao){
          //login não existe          
          alert('Login inválido!')
        }else{
          //erro de validação          
          let erros = '';
          for (let erro of Object.values(response.data)) {
            erros += erro +" "+" \n";
          }
          alert(erros)
        }
      })
      .catch(e => {
        console.log(e)
        alert("Tente novamente mais tarde!");
        
      })        
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
