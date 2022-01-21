<template>
	<div id="app">
		<HomePage v-if="currentView === 'home'" :cards="cards" @toggleActive="toggleActive" @changeView="currentView = 'AddCard'"/>
		<AddCardPage v-else @toHome="currentView ='home'" @card="saveCard"/>
	</div>
</template>

<script>
import HomePage from "./views/HomePage.vue";
import AddCardPage from "./views/AddCardPage.vue";

export default {
	name: "App",
	components: {
		HomePage,
		AddCardPage,
	},
	data() {
		return {
			currentView: "home",
			cards: [
				// {
				// 	vendor: "Bitcoin Inc",
				// 	cardNumber: "123523 123",
				// 	cardHolder: "mr Bruh",
				// 	expireMonth: "02",
				// 	expireYear: 23,
				// 	CCV: 212,
				// 	active: false,
				// },
				// {
				// 	vendor: "Evil Corp",
				// 	cardNumber: "1233 5212 2331 1234",
				// 	cardHolder: "mr Bbruh",
				// 	expireMonth: "02",
				// 	expireYear: 23,
				// 	CCV: 212,
				// 	active: false,
				// },
				// {
				// 	vendor: "Ninja Bank",
				// 	cardNumber: "123521212333 123",
				// 	cardHolder: "mr Babruh",
				// 	expireMonth: "02",
				// 	expireYear: 23,
				// 	CCV: 212,
				// 	active: false,
				// },
				// {
				// 	vendor: "Blockchain Inc",
				// 	cardNumber: "1235212125s333 123",
				// 	cardHolder: "DAVID LUNDHOLM",
				// 	expireMonth: "02",
				// 	expireYear: 23,
				// 	CCV: 212,
				// 	active: false,
				// },
			],
		};
	},
	methods: {
		saveCard(card){
			this.cards.push(card)
		},
		toggleActive(index) {
			for (const elem of this.cards) {
				if (elem.active === true) {
					elem.active = false;
				}
			}
			this.cards[index].active = !this.cards[index].active;
		},
	},
};
</script>

<style lang="scss">
body{
  min-height: 100vh;
  margin: 0;
	padding: 0;
}



</style>
