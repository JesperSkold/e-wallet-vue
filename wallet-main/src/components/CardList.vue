<template>
	<div>
		<ul v-for="(card, i) in cards" :key="card.cardNumber">
			<CardItem v-if="card.active" :card="card" class="active" />
			<CardItem :card="card" @activeCard="toggleActive" :layerIndex="'layer' + ' l-' + i" :index="i" />
		</ul>
	</div>
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
	},
};
</script>

<style lang="scss" scoped></style>
