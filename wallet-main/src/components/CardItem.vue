<template>
	<!-- <li @click="$emit('activeCard', index)" :style="{ background: cardColor }" :class="layerIndex"> -->
	<li @click="$emit('activeCard', index)" :style="{ background: cardColor }" :class="layerIndex">
		<img src="../assets/bitcoin.svg" alt="" class="vendor">
		<div class="chip-signal-box">
		<img src="../assets/wifi.svg" alt="" class="signal">
		<img src="../assets/chip.svg" alt="" class="chip">
		</div>
		<p class="card-number">{{ card.cardNumber }}</p>
		<div class="bottom-text">
		<div class="card-holder">
		<p class="name">CARDHOLDER NAME</p>
		<p class="real-name">{{ card.cardHolder }}</p>
		</div>
		<div class="valid-text">
		<p class="valid-until">VALID UNTIL</p>
		<p class="valid-expire">{{ card.expireMonth }}/{{ card.expireYear }}</p>
		</div>
		</div>
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
$maxCards: 50;
@for $i from 0 through $maxCards {
	.l-#{$i} {
		position: absolute;
		top: 30rem + ($i * 7);
		-webkit-box-shadow: 5px 5px 25px -6px rgba(0, 0, 0, 0.22);
		box-shadow: 5px 5px 25px -6px rgba(0, 0, 0, 0.22);
	}
}

// .l-14 {
//   margin-top: 40rem;
//   position: static;
// }

li {
	color: white;
	border: 1px black solid;
	width: 35rem;
	list-style: none;
	left: 0;
	right: 0;
	margin-left: auto;
	margin-right: auto;
	border-radius: 1rem;
}


.active {
	-webkit-box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
	-moz-box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
	box-shadow: 0px 0px 105px 15px rgba(255, 213, 46, 0.9);
}

.vendor {
	margin: .5rem 0 0 30rem;
}

.chip{
	background: white;
	border-radius: .5rem;
}

.chip-signal-box{
	display: flex;
	margin-left: 1rem;
	flex-direction: column;
	width: 4rem;
}

.card-number {
	margin: .5rem;
	padding: 0;
	font-size: 3rem;
	text-align: center;
	letter-spacing: 0.3rem;
}

.card-holder p {
margin: 0;
padding: 0;
}

.card-holder .name {
	margin: .5rem 0;
}

.real-name {
	font-size: 1.5rem;
}

.bottom-text {
	display: flex;
	margin: 1rem;
	justify-content: space-between;
}
.valid-text .valid-until{
	margin: .5rem 0;
}

.valid-expire {
text-align: end;
font-size: 1.5rem;
}
.valid-text p {
	padding: 0;
	margin: 0;
}
</style>
