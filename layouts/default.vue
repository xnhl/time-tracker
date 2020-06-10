<template>
	<div :class="mode">
		<img id="theme" src="/icons/sun.svg" alt="theme" @click="changeTheme">
		<nuxt />
	</div>
</template>

<script>
export default {
	data() {
		return {
			mode: 'light'
		}
	},
	head() {
		return {
			title: '',
			meta: [
				{
					hid: 'description',
					name: 'description',
					content: ''
				},
				{
					charset: 'utf-8'
				},
				{
					name: 'viewport', 
					content: 'width=device-width, initial-scale=1'
				}
			]
		}
	},
	methods: {
		changeTheme: function() {
			this.mode = this.mode === 'light' ? 'dark' : 'light';
			let root = document.documentElement;
			if (this.mode === 'light') {
				root.style.setProperty('--theme-bg', '#CCCCCC');
				localStorage.setItem("theme", "light")
			} else if (this.mode === 'dark') {
				root.style.setProperty('--theme-bg', '#141414');
				localStorage.setItem("theme", "dark")
			}
		}
	}
}
</script>

<style lang="sass">
@keyframes fadeIn
	0%
		opacity: 0
	100%
		opacity: 1
.hide
	display: none !important
@font-face
	font-family: 'Open Sans'
	src: url('../static/fonts/OpenSans-Regular.ttf') format('truetype')
	font-weight: normal
	font-style: normal
.light
	--theme-bg: #CCCCCC
	--theme-icon: invert(0)
	--theme-blue: rgba(0, 0, 255, 0.5)
	--theme-divider: linear-gradient(to right, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.75), rgba(0, 0, 0, 0))
	--theme-white: rgba(255, 255, 255, 0.9)
	--theme-black: rgba(0, 0, 0, 0.9)
	--theme-blackLight: rgba(0, 0, 0, 0.75)
	--theme-whiteBG: #dfdfdf
	--theme-itemWhite: #e6e6e6
	--gray-two: #eee
	--gray-three: #ddd
	--gray-four: #ccc
	--gray-five: #bbb
	--gray-six: #aaa
	--theme-boxShadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.05), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
	--theme-boxShadowHover: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.15), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.25) inset
	--theme-boxShadowLight: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.025), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
.dark
	--theme-bg: #141414
	--theme-icon: invert(1)
	--theme-blue: rgba(140, 139, 0, 0.5)
	--theme-divider: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 0.75), rgba(255, 255, 255, 0))
	--theme-white: rgba(0, 0, 0, 0.9)
	--theme-black: rgba(255, 255, 255, 0.9)
	--theme-blackLight: rgba(255, 255, 255, 0.75)
	--theme-whiteBG: #202020
	--theme-itemWhite: #191919
	--gray-two: #222
	--gray-three: #333
	--gray-four: #444
	--gray-five: #555
	--gray-six: #666
	--theme-boxShadow: 0 0 0.5rem 0.125rem rgba(255, 255, 255, 0.05), 0 0 0.5rem 0.25rem rgba(0, 0, 0, 0.1) inset
	--theme-boxShadowHover: 0 0 0.5rem 0.125rem rgba(255, 255, 255, 0.15), 0 0 0.5rem 0.25rem rgba(0, 0, 0, 0.25) inset
	--theme-boxShadowLight: 0 0 0.5rem 0.125rem rgba(255, 255, 255, 0.025), 0 0 0.5rem 0.25rem rgba(0, 0, 0, 0.1) inset
html
	font-family: 'Open Sans', sans-serif
	font-size: 14px
	-ms-text-size-adjust: 100%
	-webkit-text-size-adjust: 100%
	-moz-osx-font-smoothing: grayscale
	-webkit-font-smoothing: antialiased
	box-sizing: border-box
	background: #111
	position: relative
	&:root
		--theme-bg: #CCCCCC
		background: var(--theme-bg)
		transition: background 0.25s ease-in-out
*,
*:before,
*:after
	box-sizing: border-box
	font-size: 14px
	padding: 0
	margin: 0
	transition: $transition
	color: var(--theme-black)
#theme
	height: 1.25rem
	width: 1.25rem
	position: absolute
	top: 0
	right: 0
	z-index: 3
	cursor: pointer
	padding: 0.5rem
	filter: var(--theme-icon)
	box-sizing: content-box
</style>
