<template>
	<div class="newMainComp">
		<Nav v-on:getDate="onClick" />
		<div class="MainComp">
			<PhotoHolder v-bind:date="date" />
		</div>
		<Footer />
	</div>
</template>

<script>
import Nav from './Nav';
import PhotoHolder from './PhotoHolder';
import Footer from './Footer';

export default {
	name: 'MainComp',
	data() {
		return {
			date: null
		};
	},
	components: {
		Nav,
		PhotoHolder,
		Footer
	},
	methods: {
		onClick(newDate) {
			this.date = newDate;
		}
	}
};
</script>

<style scoped>
.newMainComp {
	display: flex;
	flex-direction: column;
	align-content: center;
	color: black;
	justify-content: center;
	justify-items: center;
	width: 100vw;
}
.MainComp {
	display: block;
	margin-right: auto;
	margin-left: auto;
}
</style>
