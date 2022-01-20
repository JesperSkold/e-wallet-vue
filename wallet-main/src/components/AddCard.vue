<template>
	<!-- <li @click="$emit('activeCard', index)" :style="{ background: cardColor }" :class="layerIndex"> -->
	<li @click="$emit('activeCard', index)" :style="{ background: cardColor }" :class="layerIndex">
		<p>BITCOIN/COIN</p>
		<p>SIGNAL</p>
		<p>CHIP</p>
		<p>{{ card.cardNumber }}</p>
		<p>cardholder name</p>
		<p>{{ card.cardHolder }}</p>
		<p>VALID UNTIL</p>
		<p>{{ card.expireMonth }}/{{ card.expireYear }}</p>
	</li>
</template>

<script>
export default {
	props: {
		card: Object,
		layerIndex: String,
		index: Number,
	},
	data() {
		return {
			isActive: false,
			cardColor: "",
		};
	},
	mounted() {
		switch (this.card.vendor) {
			case "Bitcoin Inc":
				this.cardColor = "yellow";
				break;
			case "Blockchain Inc":
				this.cardColor = "purple";
				break;
			case "Evil Corp":
				this.cardColor = "red";
				break;
			case "Ninja Bank":
				this.cardColor = "grey";
				break;
			default:
				this.cardColor = "black";
		}
	},
};
</script>

<style lang="scss" scoped>
// $step: 7rem;
$maxCards: 8;
@for $i from 0 through $maxCards {
	.l-#{$i} {
		position: absolute;
		top: 25rem + ($i * 2);
	}
}


// .l-14 {
//   margin-top: 40rem;
//   position: static;
// }

li {
	border: 1px black solid;
	width: 30rem;
	list-style: none;
	left: 0;
	right: 0;
	margin-left: auto;
	margin-right: auto;
  color: red;
}


// .active {  
// 	-webkit-box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
// 	-moz-box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
// 	box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
// }
</style>
