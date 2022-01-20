<template>
	<!-- <li @click="$emit('activeCard', index)" :style="{ background: cardColor }" :class="layerIndex"> -->
	<li @click="$emit('activeCard', index); setClass()" :style="{ background: cardColor }" :class="layerIndex">
		<p>BITCOIN/COIN</p>
		<p>SIGNAL</p>
		<p>CHIP</p>
		<h1>{{ card.number }}</h1>
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
    index: Number
	},
	data() {
		return {
      isActive: false,
			cardColor: "",
		};
	},
	mounted() {
		console.log(this.index);
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
// $max: 100;
// $step: 7rem;
@for $i from 0 through 50 {
	.l-#{$i} {
		top: 27rem + ($i * 7);
	}
}
// @for $i from 1 through ceil($max/$step) {
// 	$value: ($i - 1) * $step + 1;
// 	.l-#{$i} {
// 		top: $step
// 	}
// }
// @for $i from 1 through 100 {
//     @if ($i+1) % 2 == 0 {
//         .l-#{$i} {
//           top: $i +30rem
//         }
//     }
// }
// @for $i from 0 through 50 {
//   $p: 7rem;
//   $x: 27rem + $i;
//   .l-#{$i} {
//       // top: $plus+7%
//       top: $x +7
//   }
// }

li {
	border: 1px black solid;
	width: 30rem;
	list-style: none;
}
.layer {
	position: absolute;
}

.active {
	-webkit-box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
	-moz-box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
	box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
}

// .l-0 {
//   top: 27rem
// }

// .l-1{
//   top: 34rem;
// }
// .l-2{
//   top: 41rem
// }
// .l-3{
//   top: 48rem
// }

// li:nth-child(even) {
// 	list-style: none;
// 	width: 20rem;
//   z-index: 2;
// }
// li:nth-child(odd){
//   z-index: 1;
// }
</style>
