<template>
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

</template>

<script>
import CardConteudoVue from '@/components/social/CardConteudoVue';
import CardDetalheVue from '@/components/social/CardDetalheVue';
export default {
  name: 'Home',
  data () {
    return {

    }
  },
  components:{
    CardConteudoVue,
    CardDetalheVue,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
