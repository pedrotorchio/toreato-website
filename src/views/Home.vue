<script>
import Route from '@/mixins/Route.mixin';

import HeaderSection from  /** webpackChunkName: hero */'./homeSections/Header.section';

const ToSection = () => import(/* webpackChunkName: "home~to" */'./homeSections/TO.section');
const DestaquesSection = () => import( /* webpackChunkName: "home~destaques" */ './homeSections/TODestaques.section');
const MissaoSection = () => import( /* webpackChunkName: "home~missao" */'./homeSections/Missao.section');
const ServicosSection = () => import( /* webpackChunkName: "home~servicos" */'./homeSections/Servicos.section');
const LocalizacaoSection = () => import( /* webpackChunkName: "home~localizacao" */'./homeSections/Localizacao.section');
const ContatoSection = () => import( /* webpackChunkName: "home~contato" */'./homeSections/Contato.section');
const FooterSection = () => import(/* webpackChunkName: "home~footer" */'./homeSections/Footer.section');

const HoverableImage = () => import(/* webpackChunkName: "hoverable-img" */'@/components/hoverable-image');

import { progress, markerId } from '@/scripts/ScrollEvents'

export default {
  name: 'home',
  extends: Route,
  components: { 
    HeaderSection, 
    ToSection, 
    DestaquesSection, 
    MissaoSection, 
    ServicosSection, 
    LocalizacaoSection,
    ContatoSection,
    FooterSection,

    HoverableImage
  },
  data: () => ({
    activeSection: null
  }),
  methods: {
    scrollProgress() {
      window.onscroll = () => {

        const servicos = this.$refs['servicosSection'];
        const localizacao = this.$refs['localizacaoSection'];
        const contato = this.$refs['contatoSection'];
        const sobre = this.$refs['footerSection'];

        const scrollPosition = document.body.scrollTop || document.documentElement.scrollTop || window.pageYOffset;

        const scrolled = progress( servicos && servicos.$el , scrollPosition )
        const id = markerId( [  servicos && servicos.$el, 
                                  localizacao && localizacao.$el, 
                                  contato && contato.$el, 
                                  sobre && sobre.$el ], scrollPosition )

        this.$parent.setProgress(scrolled)
        this.$parent.setProgressSection(id)
         
      }  
    },
  },
  mounted() {
    setTimeout(this.scrollProgress, 0);
  }
}
</script>

<template lang="pug">
  div#sobre
    header-section#inicio( ref = "headerSection" )

    to-section#terapia-ocupacional.wide.padded( ref = "toSection" )
    
    destaques-section.wide.padded.bg-colored( )
    
    missao-section#missao.wide.half-padded.bg-colored( ref = "missaoSection" )    

    servicos-section#servicos.wide.padded.fixed( ref = "servicosSection" )

    section#img-1.space
      hoverable-image#img.cover.parallax(
        :hoverable = "false"
        src = "/assets/imgs/localizacao-4-horizontal.jpg"
        src-placeholder = "/assets/imgs/localizacao-4-horizontal-tiny.jpg" )

    localizacao-section#localizacao.wide( ref = "localizacaoSection" )

    div#photos
      ul
        li
            hoverable-image( 
              title = "Empresarial Riomar Trade Center, onde está a Reato."
              alt = "Três grandes prédios do Empresarial Riomar Trade Center, sede da Reato"
              src = "/assets/imgs/localizacao-1.jpg" src-placeholder = "/assets/imgs/localizacao-1-tiny.jpg" )
              p Empresarial
        li
            hoverable-image( 
              title = "Empresarial Riomar Trade Center ao lado do Shopping Riomar"
              alt = "Prédios do Riomar Trade Center, sede da Reato, ao lado do Shopping Riomar"
              src = "/assets/imgs/localizacao-2.jpg" src-placeholder = "/assets/imgs/localizacao-2-tiny.jpg" )
              p Empresarial/
                br
                | Shopping
        li
            hoverable-image( 
              title = "Saguão do Empresarial Riomar Trade Center"
              alt = "Saguão do Empresarial que sedia a Reato"
              src = "/assets/imgs/localizacao-3.jpg" src-placeholder = "/assets/imgs/localizacao-3-tiny.jpg" )
              p Saguão
        li
            hoverable-image( 
              title = "Recepção da Reato"
              alt = "Recepção da Reato"
              src = "/assets/imgs/localizacao-5.jpg" src-placeholder = "/assets/imgs/localizacao-5-tiny.jpg" )
              p Recepção
        li
            hoverable-image( 
              title = "Consultório de reabilitação da Reato"
              alt = "Consultório de reabilitação da Reato"
              src = "/assets/imgs/localizacao-4.jpg" src-placeholder = "/assets/imgs/localizacao-4-tiny.jpg" )
              p Consultório 2
        li
            hoverable-image( 
              title = "Consultório de atividades da Reato"
              alt = "Consultório de atividades da Reato"
              src = "/assets/imgs/localizacao-6.jpg" src-placeholder = "/assets/imgs/localizacao-6-tiny.jpg" )
              p Consultório 1
    
    contato-section#contato.wide.full-height.bg-colored.padded.fixed( ref = "contatoSection" )
    
    footer-section#sobre.full-height( ref = "footerSection" )

</template>
<style lang="sass" scoped>
@import '~media-query-mixins'
$to-height: 600px
#terapia-ocupacional
  +sm
    height: $to-height

#img-1
  height: 300px
#missao
  // height: $to-height/2
  // height: calc(100vh - #{$to-height})

.space
  margin: 100px 0

#photos
  bottom: 0
  width: 100%

  ul
    display: block
    padding: 0
    +sm
      display: flex

  li
      list-style: none
      cursor: pointer
      margin: 50px 0
      padding: 10px 10px
      box-shadow: 0px 0px 7px #00000033;

      +sm
        min-width: 64px
        flex: 1 1 auto
        padding: 0
        margin: 0
        box-shadow: none

  .hoverable-image
      padding-bottom: 100%

      /deep/ .caption
        transition: opacity .5s
        opacity: 0
        color: white
        font-weight: bold
        position: absolute
        left: 1em
      &:hover /deep/ .caption
        opacity: 1
</style>
