<template>
  <main>
    <section class="left-side">
      <form>
        <h3>Bill</h3>
        <input
          class="bill-input big-input"
          type="number"
         @change="handleChange"
          v-model="bill"
          placeholder="enter bill"
        />
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
            
            v-model="customTip"
            @change="handleChange"
            min="1"
            max="5000"
          />
        </div>
        <h3>Number of People</h3>
        <input
          class="nr-people-input big-input"
          type="number"
          min="1"
          max="50"
         @change="handleChange"
          v-model="numOfPeople"
          required="true"
        />
        <span style="color: red">{{ fieldErrors.numOfPeople }}</span>
      </form>
    </section>
    <section class="right-side">
      <div class="amount">
        <div class="tip-amount-text">
          <h3>Tip Amount</h3>
          <p>/ person</p>
        </div>
        <h2>${{ tipAmountString }}</h2>
      </div>
      <div class="amount">
        <div class="total-amount-text">
          <h3>Total</h3>
          <p>/ person</p>
        </div>
        <h2 >${{ totalString }}</h2>
      </div>
      <div class="reset-btn" @click="resetValues">
        <h4>Reset</h4>
      </div>
    </section>
  </main>
</template>

<script lang="ts" setup>
import { computed, ref, defineComponent, onMounted } from "vue";
onMounted(() => resetValues());

let tips = [
  { id: 1, percent: 5 },
  { id: 2, percent: 10 },
  { id: 3, percent: 15 },
  { id: 4, percent: 25 },
  { id: 5, percent: 50 },
];
let fieldErrors = {
  numOfPeople: undefined,
};

const bill = ref(0);
const customTip = ref(0);
const selectedTip = ref(0);
const total = ref(0);
const numOfPeople = ref(1);
const tipAmount = ref(0);
const totalString = ref("");
const tipAmountString = ref("");


const handleChange=()=>{
  if(customTip.value===0){
    giveResults(selectedTip.value)
    console.log('tip is' + selectedTip.value)
  }
    giveResults(customTip.value/100)
    console.log('custom tip is' + selectedTip.value)
  
}
const tipPercentageValue = (percentage: number) => {
  selectedTip.value = percentage/100;
  giveResults(selectedTip.value)
  customTip.value=0
};
const giveResults = (e:number) => {
  if(e===0){ totalString.value = (0).toFixed(2);
  tipAmountString.value = (0).toFixed(2);
   return}
    if(numOfPeople.value===0){ totalString.value = (0).toFixed(2);
  tipAmountString.value = (0).toFixed(2);
   return}
  total.value =
    (bill.value + bill.value * e) / numOfPeople.value;
  tipAmount.value = (bill.value * e) / numOfPeople.value;
  tipAmountString.value = tipAmount.value.toFixed(2);
  totalString.value = total.value.toFixed(2);
};
const resetValues = () => {
  bill.value = 0;
  selectedTip.value = 0;
  total.value = 0;
  tipAmount.value = 0;
  giveResults(selectedTip.value);

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
 .big-input{
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
 margin: auto;
  border-radius: 5px;
  padding: 0.5rem;
  line-height: 0;
  text-align: center;
  width: 95%;
}
h4{
  padding: 1em 2em;
  margin: 0;
   
}
@media screen and (max-width: 900px) {
  main{
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
.right-side{
  width: 100%;
  padding:0;
  margin:0; 
  padding-bottom: 2em;
}
.right-side>*{
  padding-inline: 1em;
}
.reset-btn{margin:auto;
width: 85%;}
  section.left-side{
    width: 85%;
  }
  .big-input{
    width: 90%;
  }
}
</style>
