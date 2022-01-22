<template>
	<div @click="$emit('activeCard', index)" :style="{ background: cardColor, color: textColor }" :class="layerIndex">
		<img v-if="card.vendor" :src="require(`../assets/${card.vendor}.svg`)" alt="currency" class="vendor" />
		<div class="chip-signal-box">
			<img src="../assets/wifi.svg" alt="" class="signal" />
			<img src="../assets/chip.svg" alt="" class="chip" />
		</div>
		<p class="card-number">{{ numberFormatting }}</p>
		<div class="bottom-text">
			<div class="card-holder">
				<p class="name">CARDHOLDER NAME</p>
				<p class="real-name">{{ card.cardHolder }}</p>
			</div>
			<div class="valid-text">
				<p class="valid-until">VALID UNTIL</p>
				<p class="valid-expire">{{ card.expireMonth }} / {{ card.expireYear }}</p>
			</div>
		</div>
	</div>
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
			textColor: "",
			cardColor: "",
		};
	},
	computed: {
		numberFormatting() {
			if (this.card.cardNumber) {
				return this.card.cardNumber.match(/.{1,4}/g).join(" ");
			}
			return "";
		},
	},
	mounted() {
		switch (this.card.vendor) {
			case "bitcoin":
				this.cardColor = "#FFB84D";
				this.textColor = "black" 
				break;
			case "blockchain":
				this.cardColor = "#8B58F9";
				this.textColor = "white" 
				break;
			case "evil":
				this.cardColor = "#F33355";
				this.textColor = "white" 
				break;
			case "ninja":
				this.cardColor = "#222222";
				this.textColor = "white" 
				break;
			default:
				this.cardColor = "grey";
		}
	},
};
</script>

<style lang="scss" scoped>
// $step: 7rem;
$maxCards: 100;
@for $i from 0 through $maxCards {
	.l-#{$i} {
		position: absolute;
		top: 30rem + ($i * 7);
		-webkit-box-shadow: 5px 5px 25px -6px rgba(0, 0, 0, 0.22);
		box-shadow: 5px 5px 25px -6px rgba(0, 0, 0, 0.22);
	}
}

.layer, .active {
	color: white;
	border: 1px black solid;
	width: 35rem;
	left: 0;
	right: 0;
	margin-left: auto;
	margin-right: auto;
	border-radius: 1rem;
}

.vendor {
	margin: 0.5rem 0 0 30rem;
}

.chip {
	background: white;
	border-radius: 0.5rem;
}

.chip-signal-box {
	display: flex;
	margin-left: 1rem;
	flex-direction: column;
	width: 4rem;
}

.card-number {
	height: 3rem;
	margin: 0.5rem;
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
	margin: 0.5rem 0;
}

.real-name {
	font-size: 1.5rem;
}

.bottom-text {
	display: flex;
	margin: 1rem;
	justify-content: space-between;
}
.valid-text .valid-until {
	margin: 0.5rem 0;
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
