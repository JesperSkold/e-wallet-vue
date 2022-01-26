<template>
	<div @click="$emit('activeCard', index)" :style="{ background: vendorColorHandler, color: textColorHandler }" :class="layerIndex" class="card">
		<img v-if="card.vendor" :src="require(`../assets/${card.vendor}.svg`)" alt="currency" class="vendor" />
		<div v-else class="vendor-placeholder"></div>
		<div class="chip-signal-box">
			<img v-if="card.vendor === 'bitcoin' || card.vendor === 'ninja'" src="../assets/wifi_white.svg" alt="" class="signal" />
			<img v-else src="../assets/wifi.svg" alt="wifi" class="signal" />
			<img src="../assets/chip.svg" alt="wifi" class="chip" />
		</div>
		<img v-if="index !== undefined" src="../assets/delete.svg" alt="trashcan" srcset="" class="delete" @click.stop="$emit('delete', index)" />
		<p class="card-number">{{ numberFormatting }}</p>
		<div class="bottom-text">
			<div class="card-holder">
				<p class="name">CARDHOLDER NAME</p>
				<p class="real-name">{{ card.cardHolder.toUpperCase() }}</p>
			</div>
			<div class="valid-text">
				<p class="valid-until">VALID UNTIL</p>
				<p v-if="card.expireMonth === '' && card.expireYear === ''" class="valid-expire">MM / YY</p>
				<p v-else class="valid-expire">{{ card.expireMonth }} / {{ card.expireYear }}</p>
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
	computed: {
		numberFormatting() {
			if (this.card.cardNumber) {
				return this.card.cardNumber.match(/.{1,4}/g).join(" ");
			}
			return "";
		},
		vendorColorHandler() {
			if (this.card.vendor === "bitcoin") {
				return "#FFB84D";
			} else if (this.card.vendor === "blockchain") {
				return "#8B58F9";
			} else if (this.card.vendor === "evil") {
				return "#F33355";
			} else if (this.card.vendor === "ninja") {
				return "#222222";
			} else {
				return "#d0d0d0";
			}
		},
		textColorHandler() {
			if (this.card.vendor === "bitcoin") {
				return "black";
			} else if (this.card.vendor === "blockchain") {
				return "white";
			} else if (this.card.vendor === "evil") {
				return "white";
			} else if (this.card.vendor === "ninja") {
				return "white";
			} else {
				return "black";
			}
		},
	},
};
</script>

<style lang="scss" scoped>
$maxCards: 75;
@for $i from 0 through $maxCards {
	.l-#{$i} {
		position: absolute;
		top: 25rem + ($i * 7);
		-webkit-box-shadow: 5px 5px 25px -6px rgba(0, 0, 0, 0.22);
		box-shadow: 5px 5px 25px -6px rgba(0, 0, 0, 0.22);
	}
}

.card {
	transform: scale(0.8);
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
.vendor-placeholder {
	height: 4.8rem;
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

.delete {
	width: 3rem;
	cursor: pointer;
	position: absolute;
	margin-left: 37rem;
	top: 3rem;
	&:hover {
		opacity: 0.7;
	}
}

@media screen and (max-width: 425px) {
	.card {
		left: unset;
		right: unset;
		margin-left: unset;
		margin-right: unset;
		transform: scale(0.42);
		position: absolute;
	}
	.delete {
		margin-left: 36rem;
	}
	.card-number {
		font-size: 2.9rem;
	}
}
</style>
