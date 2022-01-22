<template>
	<section>
		<div v-for="(card, i) in cards" :key="card.cardNumber" class="card-container" >
			<CardItem v-if="card.active" :card="card" class="active" />
			<CardItem :card="card" @activeCard="toggleActive" :layerIndex="'layer' + ' l-' + i" :index="i"/>
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
  }
};
</script>

<style lang="scss" scoped>
section{
  min-height: 30vh;
	margin: 0;
	padding: 0;
	position: relative;

  .card-container{
    min-width: 95vw;
    margin: 0;
    padding: 0;
  }
}

.active {
	-webkit-box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
	-moz-box-shadow: 0px 0px 105px 45px rgba(255, 213, 46, 0.9);
	box-shadow: 0px 0px 105px 15px rgba(255, 213, 46, 0.9);
}

</style>
