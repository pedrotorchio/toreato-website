<script>
import { TweenMax, SlowMo } from 'gsap';
import lazyImage from 'v-lazy-image/src';
// import '@/components/svg/about-hero-line2';
import Section from '@/mixins/Section.mixin';
import { md, min } from 'media-query-mixins/_mixins'

export default {
    extends: Section,
	components: { lazyImage },
	data: () => ({
		ctaText: "Conheça a REATO"
	}),
	computed: {
		ctaTextArray() {
			return this.ctaText.split('');
		}
	},
	methods: {
		initializeLine() {
			const el = this.$refs['line'].$el.querySelector('path');

			const length = el.getTotalLength();
			
			TweenMax.set(el, {
				visibility: 'visible',
				strokeDasharray: length,
				strokeDashoffset: length
			});

			return el;
		},
		getTimelineParameters() {
			const { result: delay } = md(()=>3) || min(()=>0);
			
			return { delay };
		},
		animate(timeline) {
			// const line = this.initializeLine();
			const ctaOffset = 0;

			timeline
				// .to(line, 1, {
				// 	strokeDashoffset: 0,
				// 	ease: SlowMo.ease.config(0.5, 0.7, false),
				// 	immediateRender: false
				// })
				// .set(this.$refs['cta'], {
				// 	visibility: 'visible'
				// }, ctaOffset)
				.addCallback(() => {
					this.$refs['cta'].style['visibility'] = 'visible';

					['Bottom', 'Left', 'Top', 'Right']
						.forEach( pos => this.$refs[`ctaBorder${pos}`].classList.add('shown') )
				}, ctaOffset)
				.staggerFrom( this.$refs['ctaLetters'], 1, { 
					autoAlpha:0, 
					y: 50, 
					ease: SlowMo.easeOut 
				}, 0.05, ctaOffset);
				
			
		},
	}
}
</script>

<template lang="pug">
	header.section
		lazy-image.cover(
			src = "/assets/imgs/about-hero-60.jpg"
			srcset = `
				/assets/imgs/about-hero-20.jpg 360w,
				/assets/imgs/about-hero-30.jpg 540w,
				/assets/imgs/about-hero-40.jpg 769w,
				/assets/imgs/about-hero-60.jpg 1200w,
				/assets/imgs/about-hero.jpg 1800w`
			src-placeholder = "/assets/imgs/about-hero-tiny.jpg"
			use-picture )
			source( 
				media="(orientation: portrait)"
				srcset = `
				/assets/imgs/about-hero-20-port.jpg 360w,
				/assets/imgs/about-hero-30-port.jpg 540w,
				/assets/imgs/about-hero-40-port.jpg 769w,
				/assets/imgs/about-hero-60.jpg 1024w,
				/assets/imgs/about-hero-port.jpg 1200w` 
				srcset-placeholder = `/assets/imgs/about-hero-port-tiny.jpg` )
				
			source( 
				media="(orientation: landscape)"
				srcset = `
				/assets/imgs/about-hero-20.jpg 360w,
				/assets/imgs/about-hero-30.jpg 540w,
				/assets/imgs/about-hero-40.jpg 769w,
				/assets/imgs/about-hero-60.jpg 1200w,
				/assets/imgs/about-hero.jpg 1800w`
				srcset-placeholder = `/assets/imgs/about-hero-tiny.jpg` )
		//- svgicon#header-line.site-line( ref = "line" name = "about-hero-line2" :fill = "false" color = "blue" )
	  
		a.cta( ref = "cta" href = "#terapia-ocupacional" )
			span.border.top( ref = "ctaBorderTop" )
			span.border.bottom( ref = "ctaBorderBottom" )
			span.border.left( ref = "ctaBorderLeft" )
			span.border.right( ref = "ctaBorderRight" )

			span.text( ref = "ctaLetters" v-for = "( letter, i ) in ctaTextArray" :key = "letter + i" :data-index = "i" ) {{ letter }}
</template>


<style lang="sass" scoped>
@import '~@/styles/config'
@import '~media-query-mixins'

header
	height: 100vh
    
header .cover 
	/deep/ img
		+cover
		object-position: 35% center
		object-fit: cover

#header-line
	position: absolute
	z-index: 555
	width: 100%
	height: 100%
	bottom: 0px
	left: 0
	top: 0
	

	
.cta
	position: absolute
	bottom: 100px
	width: calc(90% - 60px)
	left: 10px
	margin: 0 auto	
	font-size: 20px
	text-align: center
	+sm
		left: initial
		right: 100px
		margin: 0
		font-size: 24px
		width: auto
		transform: none

	+md
		right: 64px
</style>