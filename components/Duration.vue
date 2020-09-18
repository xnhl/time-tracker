<template>
	<div class="duration" :id="`${getTitle}_component`">
		<p class="duration-title" v-text="getTitle"></p>
		<div class="duration-ticks-wrapper">
			<div class="duration-fill" :style="`width: ${this.progress}%`"></div>
			<div class="duration-ticks" :style="`grid-template-columns: repeat(${this.ticks}, 1fr)`">
				<div class="duration-tick" v-for="(duration, index) in this.ticks" :key="index"></div>
			</div>
			<div class="duration-ticks-grouped" v-if="groupTicks !== 0" :style="`grid-template-columns: repeat(${this.groupTicks}, 1fr)`">
				<div class="duration-tick-grouped" v-for="(subduration, index) in this.groupTicks" :key="index"></div>
			</div>
		</div>
		<div class="duration-labels-wrapper" :data-duration="this.duration">
			<div class="duration-label" v-for="(duration, index) in this.ticks" :key="index" v-text="`${parseInt(index) + 1}`"></div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Duration',
	props: {
		duration: "",
		ticks: 0,
		groupTicks: 0,
		progress: 0
	},
	data() {
		return {
			labels: {}
		}
	},
	computed: {
		getTitle: function() {
			let stepone = this.duration.split("")[0].toUpperCase()
			let steptwo = `${stepone}${this.duration.substring(1)}`
			return steptwo
		}
	}
}
</script>

<style lang="sass">
.duration
	margin: 0.5rem
	padding: 0.5rem
	position: relative
	border-radius: 0.25rem
	box-shadow: var(--theme-boxShadow)
	background: var(--theme-itemWhite)
	.duration-title
		padding: 0.25rem
	.duration-ticks-wrapper
		position: relative
		height: 100%
		width: 100%
		height: 2rem
		border-radius: 0.25rem
		filter: var(--theme-icon)
		border: 0.05rem solid rgba(black, 0.5)
		.duration-fill
			height: 100%
			background: var(--theme-blue)
		.duration-ticks
			height: 100%
			width: 100%
			position: absolute
			top: 0
			left: 0
			z-index: 2
			display: grid
			background: transparent
			.duration-tick
				border-right: 0.025rem solid rgba(black, 0.75)
				&:last-child
					border-right: 0.025rem solid rgba(black, 0)
		.duration-ticks-grouped
			display: grid
			height: 100%
			width: 100%
			z-index: 2
			position: absolute
			top: 0
			left: 0
			background: transparent
			.duration-tick-grouped
				border-right: 0.05rem solid rgba(black, 1)
				&:last-child
					border-right: 0.05rem solid rgba(black, 0)
	.duration-labels-wrapper
		@include flexCenter
		.duration-label
			@include flexCenter
			justify-content: flex-end
			flex: 1
			padding: 0.25rem 0.1rem 0.25rem 0.25rem
			font-size: 0.75rem
	.duration-labels-wrapper[data-duration='year'], .duration-labels-wrapper[data-duration='month'], .duration-labels-wrapper[data-duration='week']
		.duration-label
			justify-content: flex-start
			padding: 0.25rem 0.25rem 0.25rem 0.1rem
	.duration-labels-wrapper[data-duration='month']
		.duration-label
			@media (max-width: 40rem)
				display: none
			&:nth-child(odd)
				@media (max-width: 40rem)
					display: flex
	.duration-labels-wrapper[data-duration='day']
		.duration-label
			@media (max-width: 30rem)
				display: none
			&:nth-child(3n)
				@media (max-width: 30rem)
					display: flex
	.duration-labels-wrapper[data-duration='hour'], .duration-labels-wrapper[data-duration='minute']
		.duration-label
			@media (max-width: 65rem)
				display: none
			&:nth-child(5n)
				@media (max-width: 65rem)
					display: flex
</style>
