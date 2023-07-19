<template>

    <site-template>
      <span slot="menuesquerdo">
        <img src="https://www.designerd.com.br/wp-content/uploads/2013/06/criar-rede-social.png" class="responsive-img">
      </span>
      <span slot="principal">
        <h2>Perfil</h2>
        <input type="text" placeholder="Nome" v-model="name">
        <input type="text" placeholder="E-mail" v-model="email">
        <input type="password" placeholder="Senha" v-model="password">
        <input type="password" placeholder="Confirme sua senha" v-model="password_confirmation">
        <button class="btn" v-on:click="cadastro()">Enviar</button>
        <router-link to="/login" class="btn orange">Já tenho conta</router-link>
      </span>
    </site-template>
  
  
  </template>
  
  <script>
  import axios from 'axios';
  import SiteTemplate from '@/templates/SiteTemplate';
  
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
      SiteTemplate,
    },
    
      
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  
  </style>
  