<template>
	<main>
		<h1>E-WALLET</h1>
		<h5>ACTIVE CARD</h5>
		<h5>{{checkIfActives}}</h5>
		<CardList :cards="cards" @toggleActive="toggleActive" />
		<button>ADD A NEW CARD</button>
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
        if (obj.active === true) {
          return ""
        }
      }
  return "You dont have an active card yet, pick a card to activate it!"
}
	},
};
</script>

<style lang="scss" scoped>
main {
	margin: 0;
	padding: 0;
	min-height: 100vh;
	position: relative;
	display: flex;
	flex-direction: column;
	align-items: center;
	h5,h1 {
		margin: 0;
		padding: 0;
	}
	h1{
		margin-top: 2rem;
	}
}

button {
	cursor: pointer;
	margin-top: 2%;
	position: relative;
	height: 4rem;
	width: 35rem;
	font-size: 1.6rem;
	border-radius: .5rem;
	background: none;
}
</style>
