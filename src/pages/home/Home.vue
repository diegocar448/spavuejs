<template>

  <site-template>

    <span slot="menuesquerdo">
      <div class="row valign-wrapper">
        <grid-vue tamanho="4">
          <img :src="usuario.imagem" :alt="usuario.name" class="circle responsive-img"> <!-- notice the "circle" class -->
        </grid-vue>
        <grid-vue tamanho="8">
          <span class="black-text">
            <h5>{{ usuario.name }}</h5>
            Add the "circle" class to it to make it appear circular.
          </span>
        </grid-vue>
      </div>
    </span>

    <span slot="principal">
      <publicar-conteudo-vue :usuario="usuario" />

      <card-conteudo-vue perfil="https://materializecss.com/images/yuna.jpg"
      nome="Maria"
      data="28/06/2023 11:42" >
        <card-detalhe-vue
          img="https://materializecss.com/images/yuna.jpg"
          titulo="teste"
          txt="I am a very simple card. I am good at containing small bits of information.
          I am convenient because I require little markup to use effectively."
          />
      </card-conteudo-vue>
    </span>



  </site-template>

</template>

<script>
import SiteTemplate from '@/templates/SiteTemplate';
import CardConteudoVue from '@/components/social/CardConteudoVue';
import CardDetalheVue from '@/components/social/CardDetalheVue';
import PublicarConteudoVue from '@/components/social/PublicarConteudoVue';
import GridVue from '@/components/layouts/GridVue';


export default {
  name: 'Home',
  data () {
    return {
      usuario:false,
    }
  },
  created(){
    let usuarioAux = sessionStorage.getItem('usuario');
    if (usuarioAux) {
      this.usuario = JSON.parse(usuarioAux);      
    }    
  },
  components:{
    SiteTemplate,
    CardConteudoVue,
    CardDetalheVue,
    PublicarConteudoVue,
    GridVue,
  },  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
