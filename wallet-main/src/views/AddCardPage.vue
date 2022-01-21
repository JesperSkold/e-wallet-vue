<template>
	<main>
		<h1>ADD NEW CARD</h1>
		<h5>NEW CARD</h5>
		<div class="card" :style="{ background: cardColor }">
			<div class="vendor-placeholder">
				<img v-if="card.vendor" :src="require(`../assets/${card.vendor}.svg`)" alt="currency" class="vendor" />
			</div>
			<div class="chip-signal-box">
				<img src="../assets/wifi.svg" alt="" class="signal" />
				<img src="../assets/chip.svg" alt="" class="chip" />
			</div>
			<p class="card-number">{{ card.cardNumber }}</p>
			<div class="bottom-text">
				<div class="card-holder">
					<p class="name">CARDHOLDER NAME</p>
					<p class="real-name">{{ card.cardHolder }}</p>
				</div>
				<div class="valid-text">
					<p class="valid-until">VALID UNTIL</p>
					<p v-if="card.expireMonth === '' && card.expireYear === ''" class="valid-expire">MM / YY</p>
					<p v-else class="valid-expire">{{ card.expireMonth }} / {{ card.expireYear }}</p>
				</div>
			</div>
		</div>

		<form @submit.prevent="submitCard">
			<div>
				<label for="">CARD NUMBER</label>
				<input type="text" placeholder="XXXX XXXX XXXX XXXX" v-model="card.cardNumber" @focus="errors = []" />
			</div>
			<div>
				<label for="">CARDHOLDER NAME</label>
				<input type="text" placeholder="FirstName LastName" v-model="card.cardHolder" required @focus="errors = []" />
			</div>

			<div class="month-year">
				<div class="month-container">
					<label for="">MONTH</label>
					<!-- 12-->
					<!-- <input type="number" /> -->
					<select name="" id="" v-model="card.expireMonth" required>
						<option value="" disabled selected hidden></option>
						<option value="01">01</option>
						<option value="02">02</option>
						<option value="03">03</option>
						<option value="04">04</option>
						<option value="05">05</option>
						<option value="06">06</option>
						<option value="07">07</option>
						<option value="08">08</option>
						<option value="09">09</option>
						<option value="10">10</option>
						<option value="11">11</option>
						<option value="12">12</option>
					</select>
				</div>
				<div class="year-container">
					<label for="">YEAR</label>
					<!-- 21-25-->
					<!-- <input type="number" /> -->
					<select name="" id="" v-model="card.expireYear" required>
						<option value="" disabled selected hidden></option>
						<option value="22">22</option>
						<option value="23">23</option>
						<option value="24">24</option>
						<option value="25">25</option>
						<option value="26">26</option>
					</select>
				</div>
			</div>

			<div class="vendor-container">
				<label for="">VENDOR</label>
				<select select name="" id="" v-model="card.vendor" @change="changeCardColor" required>
					<option value="" disabled selected hidden></option>
					<option value="bitcoin">Bitcoin Inc</option>
					<option value="blockchain">Blockchain Inc</option>
					<option value="evil">Evil Corp</option>
					<option value="ninja">Ninja Bank</option>
				</select>
			</div>

			<ul v-if="errors.length">
				<li v-for="error in errors" :key="error">{{ error }}</li>
			</ul>
			<button @click="validateForm" type="button">ADD CARD</button>
		</form>
	</main>
</template>

<script>
export default {
	data() {
		return {
			errors: [],
			filledOutForm: false,
			cardColor: "",
			card: {
				vendor: "",
				cardNumber: "",
				cardHolder: "",
				expireMonth: "",
				expireYear: "",
				CCV: 212, //random 3 numbers function
				active: false,
			},
		};
	},
	methods: {
		changeCardColor() {
			switch (this.card.vendor) {
				case "bitcoin":
					this.cardColor = "yellow";
					break;
				case "blockchain":
					this.cardColor = "purple";
					break;
				case "evil":
					this.cardColor = "red";
					break;
				case "ninja":
					this.cardColor = "grey";
					break;
				default:
					this.cardColor = "black";
			}
		},
		submitCard() {
			console.log("yo");
			this.$emit("card", { ...this.card });
		},
		validateForm() {
			this.errors = [];
			if (this.card.cardNumber === "") {
				console.log(this.errors);
				this.errors.push("You must fill out your card number!");
			} else if (this.card.cardNumber.match(/\s+/g)) {
				this.errors.push("Fill out your card without spaces!");
			} else if (!this.card.cardNumber.match(/^\d+$/)) {
				this.errors.push("You can only have numbers in your card number!");
			}else if (this.card.cardNumber.length < 16 || this.card.cardNumber.length > 16){
				this.errors.push("Your card number needs to be exactly 12 numbers!")
			}

			if (this.card.cardHolder === "") {
				this.errors.push("You must fill out your name!");
			} else if (this.card.cardNumber.match(/^[A-Za-z]+$/)) {
				this.errors.push("You cant have numbers in your name!");
			} else if (this.card.cardHolder.length > 40) {
				this.errors.push("I'm sorry if you have a long name, but it cant be more than twenty letters!");
			}

			if (!this.errors.length) {
				this.filledOutForm = true;
					this.$emit('toHome');
					this.submitCard();
			}
		},
	},
};
</script>

<style lang="scss" scoped>
.vendor-placeholder {
	height: 4rem;
}
main {
	display: flex;
	flex-direction: column;
	align-items: center;
}
form {
	display: flex;
	flex-direction: column;
	align-items: center;
}
div select,
div input {
	box-sizing: border-box;
	width: 32rem;
	display: block;
}

.month-year {
	display: flex;
}

.year-container,
.month-container {
}
.month-container {
	margin: 0 2rem 0 0;
}
.year-container select,
.month-container select {
	width: 15rem;
}

input,
.vendor-container select,
.year-container select,
.month-container select {
	height: 2rem;
}
form > div {
	margin: 1rem;
}

button {
	cursor: pointer;
	margin-top: 2rem;
	background: none;
	font-size: 1.6rem;
	font-weight: 700;
	height: 4rem;
	width: 32rem;
	&:hover {
		color: white;
		background: black;
	}
}

.card {
	overflow: hidden;
	border-radius: 1rem;
	height: 21.8rem;
	width: 35rem;
	background: grey;
	margin-bottom: 2rem;
}
.vendor {
	margin: 0.5rem 0 0 30rem;
}

.chip {
	background: white;
	border-radius: 0.5rem;
}

.chip-signal-box {
	display: flex;
	margin-left: 1rem;
	flex-direction: column;
	width: 4rem;
}

.card-number {
	height: 3rem;
	margin: 0.5rem;
	padding: 0;
	font-size: 3rem;
	text-align: center;
	letter-spacing: 0.3rem;
}

.card-holder p {
	margin: 0;
	padding: 0;
}

.card-holder .name {
	margin: 0.5rem 0;
}

.real-name {
	font-size: 1.5rem;
}

.bottom-text {
	display: flex;
	margin: 1rem;
	justify-content: space-between;
}
.valid-text .valid-until {
	margin: 0.5rem 0;
}

.valid-expire {
	text-align: end;
	font-size: 1.5rem;
}
.valid-text p {
	padding: 0;
	margin: 0;
}
</style>
