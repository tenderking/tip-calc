<template>
	<main>
		<section class="left-side">
			<form>
				<h3>Bill</h3>
				<input
					class="bill-input big-input"
					type="number"
					v-model="billAmount"
					placeholder="enter bill"
				/>
				<span class="error" v-show="billErrorsCheck()">{{
					fieldErrors.bill
				}}</span>
				<h3>Select Tip %</h3>
				<div class="tip-percent-buttons">
					<div
						class="percent-btn"
						v-for="tip in tips"
						:key="tip.id"
						@click="tipPercentageValue(tip.percent)"
						:value="tip.percent"
					>
						{{ tip.percent }}%
					</div>

					<input
						type="number"
						@click="customTipActive = true"
						@focus="customTipActive = true"
						v-model="customTip"
						min="0"
						max="5000"
					/>
				</div>
				<span class="error" v-show="customInputErrorsCheck()">{{
					fieldErrors.customTip
				}}</span>
				<h3>Number of People</h3>
				<input
					class="nr-people-input big-input"
					type="number"
					min="1"
					max="50"
					v-model="billNumOfPeople"
					required="true"
				/>
				<span class="error" v-show="numOfPeopleErrorsCheck()">{{
					fieldErrors.numOfPeople
				}}</span>
			</form>
		</section>
		<section class="right-side">
			<div class="amount">
				<div class="tip-amount-text">
					<h3>Tip Amount</h3>
					<p>/ person</p>
				</div>
				<h2>${{ billTipAmountPerPerson }}</h2>
			</div>
			<div class="amount">
				<div class="total-amount-text">
					<h3>Total</h3>
					<p>/ person</p>
				</div>
				<h2>${{ billTotalAmountPerPerson }}</h2>
			</div>
			<div class="reset-btn" @click="billReset()">
				<h4>Reset</h4>
			</div>
		</section>
	</main>
</template>

<script lang="ts" setup>
	import { computed, ref, watch } from "vue";

	//  TIPS

	let tips = [
		{ id: 1, percent: 5 },
		{ id: 2, percent: 10 },
		{ id: 3, percent: 15 },
		{ id: 4, percent: 25 },
		{ id: 5, percent: 50 },
	];

	const customTip = ref(0);
	const customTipActive = ref(false);

	const tipSelected = ref(0);

	const tipPercentageValue = (percentage: number) => {
		customTipActive.value = false;
		customTip.value = 0;
		tipSelected.value = percentage;
		console.log(tipSelected.value);
	};
	const tipCalculated = computed(() => {
		if (customTipActive.value) return customTip.value;
		return tipSelected.value;
	});

	// BILL
	const billAmount = ref(0);
	const billNumOfPeople = ref(1);

	const billTipAmountPerPerson = computed(() => {
		return (
			(billAmount.value * tipCalculated.value) /
			(100 * billNumOfPeople.value)
		).toFixed(2);
	});
	const billTotalAmountPerPerson = computed(() => {
		const tip = parseFloat(billTipAmountPerPerson.value);
		return (billAmount.value / billNumOfPeople.value + tip).toFixed(2);
	});

	const billReset = () => {
		billAmount.value = 0;
		billNumOfPeople.value = 1;
	};

	// FIELD ERRORS
	let fieldErrors = {
		numOfPeople: "Invalid: Input must be a number between 1 and 20",
		customTip: "Invalid: Input must be a valid number",
		bill: "Invalid: Input must be a valid number",
	};
	const numOfPeopleErrorsCheck = () => {
		if (billNumOfPeople.value > 20) return true;
		if (billNumOfPeople.value < 1) return true;
		if (isNaN(billNumOfPeople.value)) return true;
		return false;
	};
	const billErrorsCheck = () => {
		if (billAmount.value > 1000000) return true;
		if (billAmount.value < 0) return true;
		if (isNaN(billAmount.value)) return true;
		return false;
	};
	const customInputErrorsCheck = () => {
		if (customTip.value > 5000) return true;
		if (customTip.value < 0) return true;
		if (isNaN(customTip.value)) return true;
		return false;
	};
</script>

<style>
	main {
		width: 60rem;
		height: auto;
		background-color: var(--c-White);
		display: flex;
		border-radius: 10px;
	}
	.left-side,
	.right-side {
		width: 50%;
		padding: 1em;
	}
	h3 {
		color: var(--c-Dark-grayish-cyan);
	}
	.right-side {
		padding-top: 2em;
		background: var(--c-very-dark-cyan);
		border-radius: 10px;
		margin: 2rem;
		display: flex;
		flex-direction: column;
		/* align-items: center; */
		justify-content: center;
	}
	.tip-percent-buttons {
		display: grid;
		grid-template-columns: 100px 100px 100px;
		grid-template-rows: 1fr 1fr;
		gap: 1rem;
	}

	.percent-btn {
		background-color: var(--c-very-dark-cyan);
		color: var(--c-White);
		padding: 0.5rem;
		border-radius: 5px;
	}
	.percent-btn:hover,
	.percent-btn:focus {
		background-color: var(--c-cyan);
		color: var(--c-very-dark-cyan);
	}

	input {
		background-color: var(--c-Light-grayish-cyan-2);
		height: 52;
		border-radius: 5px;
		border: 0;
		font: inherit;
		padding-block: 0.5rem;
		text-align: right;
		font-size: smaller;
	}
	.error {
		font-size: 1rem;
		color: red;
		padding: 0;
	}
	.bill-input {
		background-image: url(src/assets/icon-dollar.svg);
		background-repeat: no-repeat;
		background-size: 12px;
		background-position: left center;
		padding-inline: 1em;
		background-position-x: 5%;
	}
	.nr-people-input {
		background-image: url(src/assets/icon-person.svg);
		background-repeat: no-repeat;
		background-size: 12px;
		background-position: left center;
		padding-inline: 1em;
		background-position-x: 5%;
	}
	/* Chrome, Safari, Edge, Opera */
	input::-webkit-outer-spin-button,
	input::-webkit-inner-spin-button {
		-webkit-appearance: none;
		margin: 0;
	}
	.big-input {
		width: 75%;
	}

	/* Firefox */
	input[type="number"] {
		-moz-appearance: textfield;
	}

	h3,
	p {
		font-size: smaller;
	}
	p {
		color: var(--c-Dark-grayish-cyan);
		font-weight: bold;
	}
	h2 {
		color: var(--c-cyan);
	}
	.amount {
		display: flex;
		justify-content: space-between;
		line-height: 0;
	}
	.amount * h3 {
		color: var(--c-White);
	}
	.total {
		font-size: smaller;
		line-height: 1em;
	}
	.reset-btn {
		background-color: var(--c-cyan);
		color: var(--c-very-dark-cyan);
		width: 60%;
		border-radius: 5px;
		padding: 0.5rem;
		line-height: 0;
		text-align: center;
	}
	@media screen and (max-width: 900px) {
		main {
			flex-direction: column;
			margin: auto;
			width: 100%;
			justify-content: center;
			align-items: center;
			margin-bottom: 2em;
		}
		.tip-percent-buttons {
			display: grid;
			grid-template-columns: repeat(2, minmax(0, 1fr));
			grid-template-rows: 1fr 1fr 1fr;
			gap: 1rem;
		}
		.right-side {
			width: 100%;
			padding: 0;
			margin: 0;
			padding-bottom: 2em;
		}
		.right-side > * {
			padding-inline: 1em;
		}
		.reset-btn {
			margin-left: 1em;
			width: 85%;
		}
		section.left-side {
			width: 85%;
		}
		.big-input {
			width: 90%;
		}
	}
</style>
