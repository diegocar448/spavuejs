<template>
  <div class="row">
    <grid-vue class="input-field" tamanho="12">
      <input type="text" v-model="conteudo.titulo">      
      <textarea v-if="conteudo.titulo" placeholder="Conteudo" v-model="conteudo.texto" id="ConteudoID" class="materialize-textarea"></textarea>      
      <input v-if="conteudo.titulo && conteudo.texto" type="text" placeholder="Link" v-model="conteudo.link">
      <input v-if="conteudo.titulo && conteudo.texto" type="text" placeholder="Imagem" v-model="conteudo.imagem">
      <label for="ConteudoID">O que está acontecendo?</label>
    </grid-vue>
    <p class="right-align">
      <button @click="addConteudo()" v-if="conteudo.titulo && conteudo.texto" class="btn waves-effect waves-light" tamanho="2 offset-s10">Publicar</button>
    </p>
  </div>
</template>

<script>
import GridVue from '@/components/layouts/GridVue';
export default {
  name: 'PublicarConteudoVue',
  props:['usuario'],
  data(){
    return {
      conteudo: { titulo: '', texto: '', link: '', imagem: '' },
    }
  },
  components:{
    GridVue,
  },
  methods:{
    addConteudo(){      
      this.$http.post(this.$urlApi+'conteudo/adicionar', {
        titulo: this.conteudo.titulo,
        texto: this.conteudo.texto,
        link: this.conteudo.link,
        imagem: this.conteudo.imagem,
      },
      {"headers":{"authorization": "Bearer "+ this.usuario.token}}).then(response => {
        if (response.data.status) {
          console.log(response.data.conteudos);
        }
      }).catch(e => {
        console.log(e)
        alert("Erro! tente mais tarde!");
      })
    }
  }
}
</script>

<style scoped>

</style>
