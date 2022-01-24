<template>
	<main>
		<h1>ADD NEW CARD</h1>
		<img class="go-back" src="../assets/go_back.svg" alt="go back btn" @click="$emit('goBack')" />
		<h5>NEW CARD</h5>
		<div class="card" :style="{ background: cardColor, color: textColor }">
			<div class="vendor-placeholder">
				<img v-if="card.vendor" :src="require(`../assets/${card.vendor}.svg`)" alt="currency" class="vendor" />
			</div>
			<div class="chip-signal-box">
				<img v-if="card.vendor === 'bitcoin' || card.vendor === 'ninja'" src="../assets/wifi_white.svg" alt="" class="signal" />
				<img v-else src="../assets/wifi.svg" alt="" class="signal" />
				<img src="../assets/chip.svg" alt="" class="chip" />
			</div>
			<p class="card-number">{{ numberFormatting }}</p>
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
				<label for="cardNumber">CARD NUMBER</label>
				<input
					name="cardNumber"
					id="card number"
					type="text"
					placeholder="XXXX XXXX XXXX XXXX"
					v-model="card.cardNumber"
					@focus="removeSingleError"
					maxlength="16"
					required
				/>
			</div>
			<div>
				<label for="fullName">CARDHOLDER NAME</label>
				<input
					name="fullName"
					id="name"
					type="text"
					placeholder="FirstName LastName"
					v-model="card.cardHolder"
					maxlength="30"
					required
					@focus="removeSingleError"
				/>
			</div>

			<div class="month-year">
				<div class="month-container">
					<label for="months">MONTH</label>
					<!-- 12-->
					<!-- <input type="number" /> -->
					<select name="months" id="month" v-model="card.expireMonth" required @change="removeSingleError">
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
					<label for="years">YEAR</label>
					<!-- 21-25-->
					<!-- <input type="number" /> -->
					<select name="years" id="year" v-model="card.expireYear" @change="removeSingleError" required>
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
				<label for="vendor">VENDOR</label>
				<select
					name="vendor"
					id="vendor"
					v-model="card.vendor"
					@change="
						changeCardColor();
						removeSingleError($event);
					"
					required
				>
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
			textColor: "",
			card: {
				vendor: "",
				cardNumber: "",
				cardHolder: "",
				expireMonth: "",
				expireYear: "",
				CCV: this.randomCvv(),
				active: false,
			},
		};
	},
	props: {
		cards: Array,
	},
	computed: {
		numberFormatting() {
			if (this.card.cardNumber) {
				return this.card.cardNumber.match(/.{1,4}/g).join(" ");
			}
			return "";
		},
	},
	methods: {
		// preventLetter(e) {
		// 	console.log(e);
		// 	if (this.errors.includes("You cant have numbers in your name!")) {
		// 		console.log("found");
		// 		return;
		// 	}
		// 	if (!e.key.match(/\d/)) {
		// 		this.errors.push("You can only have numbers in your card number!");
		// 		e.preventDefault();
		// 	}
		// },
					
		// preventNum(e) { @keydown="preventNum($event)"
		// 	console.log(e);
		// 	this.errors.splice(this.errors.indexOf("You cant have numbers or special characters in your name!"), 1);
		// 	if (!e.key.match(/[A-Öa-ö] §/)) {
		// 		this.errors.push("You cant have numbers or special characters in your name!");
		// 		e.preventDefault();
		// 	}
		// },
		randomCvv() {
			return String(Math.floor(Math.random() * 4)) + String(Math.floor(Math.random() * 4)) + String(Math.floor(Math.random() * 4));
		},
		changeCardColor() {
			switch (this.card.vendor) {
				case "bitcoin":
					this.cardColor = "#FFB84D";
					this.textColor = "black";
					break;
				case "blockchain":
					this.cardColor = "#8B58F9";
					this.textColor = "white";
					break;
				case "evil":
					this.cardColor = "#F33355";
					this.textColor = "white";
					break;
				case "ninja":
					this.cardColor = "#222222";
					this.textColor = "white";
					break;
				default:
					this.cardColor = "grey";
			}
		},
		submitCard() {
			this.$emit("card", { ...this.card });
		},
		validateForm() {
			this.errors = [];
			if (this.card.cardNumber === "") {
				this.errors.push("You must fill out your card number!");
			} else if (this.card.cardNumber.match(/\s+/g)) {
				this.errors.push("Fill out your card without spaces!");
			} else if (!this.card.cardNumber.match(/^\d+$/)) {
				this.errors.push("You can only have numbers in your card number!");
			} else if (this.card.cardNumber.length < 16 || this.card.cardNumber.length > 16) {
				this.errors.push("Your card number needs to be exactly 12 numbers!");
			}

			if (this.card.cardHolder === "") {
				this.errors.push("You must fill out your name!");
			} else if (this.card.cardHolder.match(/[0-9!@#$%^§&*()_+\-=[\]{};':"\\|,.<>/?¨´]+/g)) {
				this.errors.push("You cant have numbers or special characters in your name!");
			} else if (this.card.cardHolder.length < 4) {
				this.errors.push("Your name must be longer than 3 letters, sorry!");
			} else if (this.card.cardHolder.length > 29) {
				this.errors.push("I'm sorry if you have a long name, but it cant be more than 29 letters!");
			}

			if (this.card.expireMonth === "") {
				this.errors.push("Select what month your card expires!");
			}

			if (this.card.expireYear === "") {
				this.errors.push("Select what year your card expires!");
			}

			if (this.card.vendor === "") {
				this.errors.push("Select a vendor!");
			}

			this.checkDupNum();

			if (!this.errors.length) {
				this.filledOutForm = true;
				this.$emit("toHome");
				this.submitCard();
				(this.cardColor = "#d0d0d0"), //resetting card render cuz of keep alive vvvvv
					(this.card.vendor = ""),
					(this.card.cardNumber = ""),
					(this.card.cardHolder = ""),
					(this.card.expireMonth = ""),
					(this.card.expireYear = ""),
					(this.card.CCV = null);
			}
		},
		removeSingleError(event) {
			for (const error of this.errors) {
				if (error.includes(event.target.id)) {
					this.errors.splice(this.errors.indexOf(error), 1);
					console.log(this.errors);
				}
			}
		},
		checkDupNum() {
			for (const value of this.cards) {
				if (this.card.cardNumber === value.cardNumber) {
					this.errors.push("A card with this number already exists!");
				}
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
h1,
h5 {
	margin: 0;
}
h5 {
	margin-bottom: 0.5rem;
}

.month-year {
	display: flex;
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
	margin: 2rem 0;
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
	border: 1px black solid;
	overflow: hidden;
	border-radius: 1rem;
	height: 21.8rem;
	width: 35rem;
	background: #d0d0d0;
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

.go-back {
	// position: absolute;
	// right: 60%;
	// bottom: 90%;
	margin-right: 31rem;
	width: 5rem;
	cursor: pointer;
	color: white;
	border-radius: 100%;
	background: none;
	&:hover {
		background: #d0d0d0;
	}
}
</style>
