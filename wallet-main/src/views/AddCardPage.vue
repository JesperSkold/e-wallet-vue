<template>
	<main>
		<h1>ADD NEW CARD</h1>
		<h5>NEW CARD</h5>
		<form action="">
			<div>
				<label for="">CARD NUMBER</label>
				<input type="text" placeholder="XXXX XXXX XXXX XXXX" />
			</div>
			<div>
				<label for="">CARDHOLDER NAME</label>
				<input type="text" placeholder="FirstName LastName" />
			</div>

			<div class="month-year">
				<div class="month-container">
					<label for="">MONTH</label>
					<!-- 12-->
					<input type="number" />
				</div>
				<div class="year-container">
					<label for="">YEAR</label>
					<!-- 21-25-->
					<input type="number" />
				</div>
			</div>

			<div class="vendor">
				<label for="">VENDOR</label>
				<select>
					<option value="" disabled selected hidden></option>
					<option value="Bitcoin Inc">Bitcoin Inc</option>
					<option value="Blockchain Inc">Blockchain Inc</option>
					<option value="Evil Corp">Evil Corp</option>
					<option value="Ninja Bank">Ninja Bank</option>
				</select>
			</div>
		</form>
		<button>ADD CARD</button>
	</main>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
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
div select, input {
  box-sizing: border-box;
  width: 20rem;
  display: block;
}

.month-year {
  display: flex;
  
}

.year-container, .month-container{
}
.month-container{
  margin: 0 2rem 0 0;

}
.year-container input, .month-container input {
}

input, .vendor select {
  height: 2rem;
}
form > div {
margin: 1rem;
}
</style>
