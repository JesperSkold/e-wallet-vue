<template>
	<div id="app">
		<HomePage :cards="cards" />
		<AddCardPage />
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
			cards: [
				{
					vendor: "Bitcoin Inc",
					cardNumber: "123523 123",
					cardHolder: "mr Bruh",
					expireMonth: "02",
					expireYear: 23,
					CCV: 212,
					active: false,
				},
				{
					vendor: "Evil Corp",
					cardNumber: "123521233 123",
					cardHolder: "mr Bbruh",
					expireMonth: "02",
					expireYear: 23,
					CCV: 212,
					active: false,
				},
				{
					vendor: "Ninja Bank",
					cardNumber: "123521212333 123",
					cardHolder: "mr Babruh",
					expireMonth: "02",
					expireYear: 23,
					CCV: 212,
					active: true,
				},
				{
					vendor: "Blockchain Inc",
					cardNumber: "1235212125s333 123",
					cardHolder: "mr Babruh",
					expireMonth: "02",
					expireYear: 23,
					CCV: 212,
					active: false,
				},
				{
					vendor: "Blockchain Inc",
					cardNumber: "1235212125ds333 123",
					cardHolder: "mr Babruh",
					expireMonth: "02",
					expireYear: 23,
					CCV: 212,
					active: false,
				},
				{
					vendor: "Ninja Bank",
					cardNumber: "1235as21212333 123",
					cardHolder: "mr Babruh",
					expireMonth: "02",
					expireYear: 23,
					CCV: 212,
					active: false,
				},
				{
					vendor: "Blockchain Inc",
					cardNumber: "12352a12125ds333 123",
					cardHolder: "mr Babruh",
					expireMonth: "02",
					expireYear: 23,
					CCV: 212,
					active: false,
				},
				{
					vendor: "Blockchain Inc",
					cardNumber: "12352121a25ds333 123",
					cardHolder: "mr Babruh",
					expireMonth: "02",
					expireYear: 23,
					CCV: 212,
					active: false,
				},
			],
		};
	},
};
</script>

<style lang="scss"></style>
