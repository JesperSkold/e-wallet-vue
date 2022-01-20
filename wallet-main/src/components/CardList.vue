<template>
	<div class="lol">
		<ul v-for="(card, i) in cards" :key="card.cardNumber" >
			<CardItem v-if="card.active" :card="card" class="active" />
			<CardItem :card="card" @activeCard="toggleActive" :layerIndex="'layer' + ' l-' + i" :index="i"/>
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
  }
};
</script>

<style lang="scss" scoped>
.lol{
	padding: 0;
	margin: 0;
  height: 85vh;
  position: relative;
//  .spacer {
//    height: 20rem;
//    width: 100%;
//  }
  ul{
		margin: 0;
		padding: 0;
    min-width: 100vw;
  }
}



// .activeContainer {
//   height: 80vh;
// }
// .spacer-container{
//   display: flex;
//  flex-flow: column;
//   height: 100rem;
// }
// .spacer{
//   flex: 1;
//   margin: 5rem;
// }

</style>
