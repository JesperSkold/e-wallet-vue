<template>
	<section>
		<div v-for="(card, i) in cards" :key="card.cardNumber" class="card-container">
			<CardItem v-if="card.active" :card="card" :style="{ 'box-shadow': activeShadowHandler }" @delete="deleteEcho" :index="i" />
			<CardItem :card="card" @activeCard="toggleActive" :layerIndex="'layer' + ' l-' + i" :index="i" @delete="deleteEcho" />
		</div>
	</section>
</template>

<script>
import CardItem from "./CardItem.vue";
export default {
	components: {
		CardItem,
	},
	props: {
		cards: Array,
	},
	methods: {
		toggleActive(index) {
			this.$emit("toggleActive", index);
		},
		deleteEcho(index) {
			console.log(index);
			this.$emit("delete", index);
		},
	},
	computed: {
		activeShadowHandler() {
			for (const obj of this.cards) {
				if (obj.active && obj.vendor === "bitcoin") {
					return "0px 22px 40px 4px rgba(250, 178, 25, 0.96) ";
				} else if (obj.active && obj.vendor === "blockchain") {
					return "0px 22px 30px 4px rgba(133, 20, 204, 0.9)";
				} else if (obj.active && obj.vendor === "evil") {
					return "0px 22px 30px 4px rgba(204, 20, 56, 0.9)";
				} else if (obj.active && obj.vendor === "ninja") {
					return "0px 22px 30px 4px rgba(31, 24, 30, 0.9)";
				}
			}
			return "";
		},
	},
};
</script>

<style lang="scss" scoped>
section {
	min-height: 30vh;
	margin: 0;
	padding: 0;
	position: relative;

	.card-container {
		min-width: 95vw;
		margin: 0;
		padding: 0;
	}
}
</style>
