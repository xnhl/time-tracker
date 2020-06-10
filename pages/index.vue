<template>
	<div id="wrapper">
		<p id="time" v-text="time"></p>
		<div class="durations-wrapper">
			<Duration :progress="this.minute" duration="minute" :ticks="60" :groupTicks="4" />
			<Duration :progress="this.hour" duration="hour" :ticks="60" :groupTicks="4" />
			<Duration :progress="this.day" duration="day" :ticks="24" :groupTicks="4" />
			<Duration :progress="this.week" duration="week" :ticks="7" :groupTicks="0" />
			<Duration :progress="this.month" duration="month" :ticks="monthLength" :groupTicks="0" />
			<Duration :progress="this.year" duration="year" :ticks="12" :groupTicks="4" />
		</div>
	</div>
</template>

<script>
import moment from 'moment'
import Duration from '@/components/Duration'
export default {
	components: {Duration},
	data() {
		return {
			time: `${moment().format("LL")} ${moment().format("LTS")}`,
			secondsElapsed: 0,
			sleepTime: "",
			minute: moment().seconds() * 1.666666666666667,
			monthLength: moment().daysInMonth(),
			hour: 0.0,
			day: 0.0,
			week: 0.0,
			month: 0.0,
			year: 0.0,
			life: {},
		}
	},
	beforeMount() {
		let now = moment();
		let dayStart = moment().startOf('day');
		let numSeconds = now.diff(dayStart, 'seconds');
		this.secondsElapsed = numSeconds;

		let dayStartUnix = moment().startOf("day").unix();
		let dayEndUnix = moment().endOf("day").unix();
		let dayNowUnix = moment().unix();
		let dayLength = dayEndUnix - dayStartUnix;
		let dayPct = ((dayNowUnix - dayStartUnix)/dayLength) * 100;
		this.day = dayPct;

		let hourStartUnix = moment().startOf("hour").unix();
		let hourEndUnix = moment().endOf("hour").unix();
		let hourNowUnix = moment().unix();
		let hourLength = hourEndUnix - hourStartUnix;
		let hourPct = ((hourNowUnix - hourStartUnix)/hourLength) * 100;
		this.hour = hourPct;
		
		let weekStartUnix = moment().startOf("week").unix();
		let weekEndUnix = moment().endOf("week").unix();
		let weekNowUnix = moment().unix();
		let weekLength = weekEndUnix - weekStartUnix;
		let weekPct = ((weekNowUnix - weekStartUnix)/weekLength) * 100;
		this.week = weekPct;
		
		let monthStartUnix = moment().startOf("month").unix();
		let monthEndUnix = moment().endOf("month").unix();
		let monthNowUnix = moment().unix();
		let monthLength = monthEndUnix - monthStartUnix;
		let monthPct = ((monthNowUnix - monthStartUnix)/monthLength) * 100;
		this.month = monthPct;
		
		let yearStartUnix = moment().startOf("year").unix();
		let yearEndUnix = moment().endOf("year").unix();
		let yearNowUnix = moment().unix();
		let yearLength = yearEndUnix - yearStartUnix;
		let yearPct = ((yearNowUnix - yearStartUnix)/yearLength) * 100;
		this.year = yearPct;
	},
	mounted() {
		setInterval(() => {
			let dayStartUnix = moment().startOf("day").unix();
			let dayEndUnix = moment().endOf("day").unix();
			let dayNowUnix = moment().unix();
			let dayLength = dayEndUnix - dayStartUnix;
			let dayPct = ((dayNowUnix - dayStartUnix)/dayLength) * 100;
			this.day = dayPct;

			let hourStartUnix = moment().startOf("hour").unix();
			let hourEndUnix = moment().endOf("hour").unix();
			let hourNowUnix = moment().unix();
			let hourLength = hourEndUnix - hourStartUnix;
			let hourPct = ((hourNowUnix - hourStartUnix)/hourLength) * 100;
			this.hour = hourPct;
			 
			let weekStartUnix = moment().startOf("week").unix();
			let weekEndUnix = moment().endOf("week").unix();
			let weekNowUnix = moment().unix();
			let weekLength = weekEndUnix - weekStartUnix;
			let weekPct = ((weekNowUnix - weekStartUnix)/weekLength) * 100;
			this.week = weekPct;
			
			let monthStartUnix = moment().startOf("month").unix();
			let monthEndUnix = moment().endOf("month").unix();
			let monthNowUnix = moment().unix();
			let monthLength = monthEndUnix - monthStartUnix;
			let monthPct = ((monthNowUnix - monthStartUnix)/monthLength) * 100;
			this.month = monthPct;
			
			let yearStartUnix = moment().startOf("year").unix();
			let yearEndUnix = moment().endOf("year").unix();
			let yearNowUnix = moment().unix();
			let yearLength = yearEndUnix - yearStartUnix;
			let yearPct = ((yearNowUnix - yearStartUnix)/yearLength) * 100;
			this.year = yearPct;

			this.time = `${moment().format("LL")} ${moment().format("LTS")}`;
			this.minute = parseInt(moment().seconds()) * 1.666666666666667;
			this.secondsElapsed++
		}, 1000);
	}
}
</script>

<style lang="sass">
#wrapper
	padding: 0.25rem
	position: relative
	@include pageWrapper
	#time
		padding: 1rem
		margin: 1rem
		font-size: 1.5rem
		@include flexCenter
	.durations-wrapper
		width: 100%
		margin: 0 auto
		padding: 0.25rem
		background: var(--theme-whiteBG)
		box-shadow: var(--theme-boxShadowLight)
		border-radius: 0.25rem
</style>
