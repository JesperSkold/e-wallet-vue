<template>
	<main>
		<h1>E-WALLET</h1>
		<h5>ACTIVE CARD</h5>
		<h5>{{ checkIfActives }}</h5>
		<h5>{{ checkIfCards }}</h5>
		<CardList :cards="cards" @toggleActive="toggleActive" @delete="saveIndex" />
		<div class="fade-layer" v-if="showModal"></div>
		<div class="modal" v-if="showModal">
			<p>Are you sure you want to remove this card?</p>
			<div class="btn-container">
				<button @click="$emit('delete', deleteIndex);showModal = false">YES</button>
				<button @click="showModal = false">NO</button>
			</div>
		</div>
		<button @click="$emit('changeView')">ADD A NEW CARD</button>
	</main>
</template>

<script>
import CardList from "../components/CardList.vue";
export default {
	components: {
		CardList,
	},
	data() {
		return {
			showModal: false,
			deleteIndex: null,
		};
	},
	props: {
		cards: Array,
	},
	methods: {
		toggleActive(index) {
			this.$emit("toggleActive", index);
		},
		saveIndex(index) {
			this.deleteIndex = index;
			this.showModal = true;
			console.log(index);
		},
	},
	computed: {
		checkIfActives() {
			for (const obj of this.cards) {
				if (obj.active === true) {
					return "";
				}
			}
			return "You dont have an active card yet, pick a card to activate it!";
		},
		checkIfCards() {
			if (this.cards.length) {
				return "";
			}
			return "You dont have any cards yet, click the add new card button to add cards.";
		},
	},
};
</script>

<style lang="scss" scoped>
.modal {
	position: fixed;
	box-shadow: 10px 10px 5px -4px rgba(0,0,0,0.75);
-webkit-box-shadow: 10px 10px 5px -4px rgba(0,0,0,0.75);
-moz-box-shadow: 10px 10px 5px -4px rgba(0,0,0,0.75);
	border-radius: 1rem;
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
	background: rgb(243, 239, 239);
	margin: auto;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	width: 30rem;
	height: 15rem;
	z-index: 999;
}
.fade-layer {
	z-index: 998;
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	background: rgba(128, 128, 128, 0.301);
}
main {
	margin: 0;
	padding: 0;
	min-height: 100vh;
	position: relative;
	display: flex;
	flex-direction: column;
	align-items: center;
	h5,
	h1 {
		margin: 0;
		padding: 0;
	}
	h5 {
		margin-bottom: 0.2rem;
	}
	h1 {
		margin: 2rem 0;
	}
}

div > button {
	cursor: pointer;
	margin: 0 1rem;
	width: 5rem;
	height: 2rem;
}

main > button {
	cursor: pointer;
	margin-top: 2%;
	position: relative;
	height: 4rem;
	width: 35rem;
	font-size: 1.6rem;
	border-radius: 0.5rem;
	background: none;
	&:hover {
		color: white;
		background: black;
	}
}
</style>
