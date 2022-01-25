<template>
	<div id="app">
		<HomePage v-if="currentView === 'home'" :cards="cards" @toggleActive="toggleActive" @changeView="currentView = 'AddCard'" @delete="deleteEcho" />
		<keep-alive>
			<AddCardPage v-if="currentView === 'AddCard'" @toHome="currentView = 'home'" @card="saveCard" @goBack="currentView = 'home'" :cards="cards" />
		</keep-alive>
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
			cards: [],
		};
	},
	methods: {
		saveCard(card) {
			this.cards.push(card);
			localStorage.setItem("cards", JSON.stringify(this.cards));
		},
		toggleActive(index) {
			for (const elem of this.cards) {
				if (elem.active === true) {
					elem.active = false;
				}
			}
			this.cards[index].active = !this.cards[index].active;
			localStorage.setItem("cards", JSON.stringify(this.cards));
		},
		deleteEcho(index) {
			console.log(index);
			this.cards.splice(index, 1);
			localStorage.setItem("cards", JSON.stringify(this.cards));
		},
	},
	created() {
		if (localStorage.cards) {
			this.cards = JSON.parse(localStorage.getItem("cards"));
		}
	},
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Saira:wght@200&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Saira:wght@200&display=swap");
body {
	min-height: 100vh;
	margin: 0;
	padding: 0;
}
h1,
h2,
h3,
h4,
h5,
h6 {
	font-family: "Source Sans Pro", sans-serif;
}
p,
label,
li {
	font-family: "PT Mono", monospace;
}
</style>
