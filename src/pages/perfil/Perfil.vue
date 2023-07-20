<template>

    <site-template>
      <span slot="menuesquerdo">
        <img src="https://www.designerd.com.br/wp-content/uploads/2013/06/criar-rede-social.png" class="responsive-img">
      </span>
      <span slot="principal">
        <h2>Perfil</h2>
        <input type="text" placeholder="Nome" v-model="name">
        <input type="text" placeholder="E-mail" v-model="email">

        <form action="#">
            <div class="file-field input-field">
            <div class="btn">
                <span>Imagem</span>
                <input type="file">
            </div>
            <div class="file-path-wrapper">
                <input class="file-path validate" type="text">
            </div>
            </div>
        </form>

        <input type="password" placeholder="Senha" v-model="password">
        <input type="password" placeholder="Confirme sua senha" v-model="password_confirmation">
        <button class="btn" v-on:click="perfil()">Atualizar</button>
        
      </span>
    </site-template>
  
  
  </template>
  
  <script>
  import axios from 'axios';
  import SiteTemplate from '@/templates/SiteTemplate';
  
  export default {
    name: 'Perfil',
    data () {
      return {
        usuario:false,
        name:'',
        email:'',
        password:'',
        password_confirmation:'',
      }
    },
    created(){
        let usuarioAux = sessionStorage.getItem('usuario');
        if (usuarioAux) {
            this.usuario = JSON.parse(usuarioAux);
            this.name = this.usuario.name;
            this.email = this.usuario.email;
        }
    },
    components:{
      SiteTemplate,
    },
    methods:{
        perfil(){
            axios.put('http://127.0.0.1:8000/api/perfil', {
                name: this.name,
                email: this.email,
                password: this.password,
                password_confirmation: this.password_confirmation,
        }, {
            "headers":{
                "authorization": `Bearer ${this.usuario.token}`
            }
        })
        .then(response => {                
            if (response.data.token) {
                //login com sucesso          
                sessionStorage.setItem('usuario', JSON.stringify(response.data))
                alert('Perfil atualizado!')
            }else{
                //erro de validação
                console.log('erros de validação')
                let erros = '';
                for (let erro of Object.values(response.data)) {
                    erros += erro +" "+" \n";
                }
                alert(erros)
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
  