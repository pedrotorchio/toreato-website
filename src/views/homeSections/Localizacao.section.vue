<script>
const hoverableImage = import(/* webpackChunkName: "hoverable-img" */'@/components/hoverable-image');

import Section from '@/mixins/Section.mixin';
import { address } from '@/contact'

export default {
    extends: Section,
    components: { hoverableImage },
    data: () => ({
        ctaText: "Como Chegar"
    }),
    computed: {
        ctaTextArray() {
            return this.ctaText.split('');
        },
        line1() {
            return `${address.street}, ${address.number}`
        },
        line2() {
            return `Sala ${address.room}`
        },
        line3() {
            return address.area
        }
    },
    methods: {
        animate( timeline ) {
            // timeline
            //     .addCallback(() => {
			// 		this.$refs['cta'].style['visibility'] = 'visible';

			// 		['Bottom', 'Left', 'Top', 'Right']
			// 			.forEach( pos => this.$refs[`ctaBorder${pos}`].classList.add('shown') )
			// 	})
			// 	.staggerFrom( this.$refs['ctaLetters'], 1, { 
			// 		autoAlpha:0, 
			// 		y: 50, 
			// 		ease: SlowMo.easeOut 
			// 	}, 0.05);
        }
    }
}
</script>
<template lang="pug">
    section#localizacao
        div.textual
            div.inner
                div.grouped
                    h2 Empresarial Riomar Trade Center
                    ul
                        li Excelente Localização
                        li Em frente ao Shopping Riomar
                        li Infra-estrutura de estacionamento com segurança e conforto
                        li Ambientes planejados para a prática da Terapia Ocupacional
                    h3 
                        | {{ line1 }}
                        br 
                        | {{ line2 }}
                        br 
                        | {{ line3 }}

                //- button.cta( ref = "cta" )
                //-     span.border.top( ref = "ctaBorderTop" )
                //-     span.border.bottom( ref = "ctaBorderBottom" )
                //-     span.border.left( ref = "ctaBorderLeft" )
                //-     span.border.right( ref = "ctaBorderRight" )

                //-     span.text( ref = "ctaLetters" v-for = "( letter, i ) in ctaTextArray" :key = "letter + i" :data-index = "i" ) {{ letter }}
        div.map-container
            iframe#map(
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3950.1408328497528!2d-34.89415618454557!3d-8.087116883102201!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x7ab1f3badda7f65%3A0x7ef167bddc90e085!2sBusiness+RioMar+Trade+Center!5e0!3m2!1sen!2sbr!4v1546819775920" 
                frameborder="0" style="border0" allowfullscreen )
</template>
<style lang="sass" scoped>
@import "~@/styles/config"
@import "~media-query-mixins"

#localizacao
    display: block
    +md
        display: flex
        align-items: stretch
    
.textual, .map-container
    width: 100%
    +md
        flex: 0 0 50%
    position: relative
.textual
    padding: 10px
    +lg
        padding: 100px
.inner
    width: 100%
    +md
        width: 470px
    margin-left: auto
    height: 100%
    display: flex
    flex-direction: column
    justify-content: space-around
    align-items: center

    font-size: 20px
    +md
        font-size: 22px

    h1, h2, button, h3
        text-align: center
        margin: 36px 0
    h1
        font-size: 1.3em
    h2
        font-size: 1.1em
    h3
        font-size: 1em
        line-height: 2em
    li
        font-size: 1em
        line-height: 2em
button
    background-color: transparent

    &:hover
        color: lighten($color--primary, 60)
.map-container
    height: 80vh
    +md
        height: auto
#map
    width: 100%
    height: 100%
</style>
