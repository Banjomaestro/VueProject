<template>
<div class="space">
	<footer>
		<h4>Built by Benjamin Amrani</h4>
	</footer>
</div>
</template>

<script>
export default {
	name: 'FooterComp'
};
</script>

<style scoped>
footer {
	position: relative;
	right: 0;
	left: 0;
	bottom: 0;
	height: 80px;
	display: flex;
	align-items: center;
	justify-content: center;
	background: rgb(17, 15, 15);
	margin-top: 100px;
	border-top: 1px solid #1f1f1f;
	width: 100vw;
}

h4 {
	color: #dfdfdf;
	font-size: 13px;
	font-weight: 400;
}
</style>
