<template>

  <login-template>
    <span slot="menuesquerdo">
      <img src="https://www.designerd.com.br/wp-content/uploads/2013/06/criar-rede-social.png" class="responsive-img">
    </span>
    <span slot="principal">
      <h2>Cadastro</h2>
      <input type="text" placeholder="Nome" v-model="name">
      <input type="text" placeholder="E-mail" v-model="email">
      <input type="password" placeholder="Senha" v-model="password">
      <input type="password" placeholder="Confirme sua senha" v-model="password_confirmation">
      <button class="btn" v-on:click="cadastro()">Enviar</button>
      <router-link to="/login" class="btn orange">Já tenho conta</router-link>
    </span>
  </login-template>


</template>

<script>
import axios from 'axios';
import LoginTemplate from '@/templates/LoginTemplate';

export default {
  name: 'Cadastro',
  data () {
    return {
      name:'',
      email:'',
      password:'',
      password_confirmation:'',
    }
  },
  components:{
    LoginTemplate,
  },
  methods:{
    cadastro(){
      return this.$http.post(this.$urlApi+'cadastro', {
        name: this.name,
        email: this.email,
        password: this.password,
        password_confirmation: this.password_confirmation,
      })
      .then(response => {
        console.log(response)
        if (response.data.usuario) {
          //login com sucesso          
          sessionStorage.setItem('usuario', JSON.stringify(response.data.usuario))
          alert("Cadastro realizado com sucesso!")
          this.$router.push('/')
        }else if(response.data.status == false && response.data.validacao){
          //login não existe
          console.log('erros de validação')
          let erros = '';
          for (let erro of Object.values(response.data.erros)) {
            erros += erro +" "+" \n";
          }
          alert(erros)          
        }else{
          //erro de validação
          alert('Erro no Cadastro! Tente novamente mais tarde')          
        }
      })
      .catch(e => {
        console.log(e)
        alert("tente novamente mais tarde!");
        
      })        
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
