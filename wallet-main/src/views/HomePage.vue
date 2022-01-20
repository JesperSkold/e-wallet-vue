<template>
	<main>
		<h1>E-WALLET</h1>
		<h5>ACTIVE CARD</h5>
		<h5>{{checkIfActives}}</h5>
		<CardList :cards="cards" @toggleActive="toggleActive" />
		<button>SADFASDFASD</button>
	</main>
</template>

<script>
import CardList from "../components/CardList.vue";
export default {
	components: {
		CardList,
	},
	props: {
		cards: Array,
	},
	data() {
		return {
			checkIfActive: null,
		};
	},
	methods: {
		toggleActive(index) {
			this.$emit("toggleActive", index);
		},
	},
	computed: {
    checkIfActives(){
      for (const obj of this.cards) {
        console.log("yo");
        if (obj.active === true) {
          return ""
        }
      }
  return "Pick a card, any card"
}
	},
};
</script>

<style lang="scss" scoped>
main {
	min-height: 100vh;
	position: relative;
	display: flex;
	flex-direction: column;
	align-items: center;
	h5 {
		margin: 0;
		padding: 0;
	}
}
button {
	margin: 1rem;
	position: relative;
}
</style>
