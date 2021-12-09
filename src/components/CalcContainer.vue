<template>
  <main>
      <section class="left-side">
<form >
    <h3>Bill</h3>
    <input type="text"> 
    <h3>Select Tip %</h3>
    <div class="tip-percent-buttons">
        <button>5%</button>
        <button>10%</button>
        <button>15%</button>
        <button>25%</button>
        <button>50%</button>
        <input type="text">
    </div>
    <h3>Number of People</h3>
    <input type="text">
</form>
      </section>
      <section class="right-side">
<div class="tip-amount">
    <div class="tip-amount-text"> 
        <h3>Tip Amount</h3>
        <p>/ person</p>
        </div>
        <h2>{{tipAmount}}</h2>

</div>
<div class="total-amount">
    <div class="total-amount-text"> 
        <h3>Total</h3>
        <p>/ person</p>
        </div>
        <h2>{{total}}</h2>
        
</div>
<div class="reset-btn">
    <h4>Reset</h4>
</div>
      </section>
  </main>
</template>

<script lang="ts" setup>
const total=0.00
const tipAmount=0.00

</script>

<style>

   main{
       width: 60rem;
       height: auto;
       background-color:var(--c-White);
       display: flex;
       border-radius: 10px;
   }
   .left-side, .right-side{
     
     width:50%;
     padding: 1em;
     }
     h3{
         color: var(--c-Dark-grayish-cyan);
     }
     .right-side{
         background: var(--c-very-dark-cyan);
         border-radius: 10px;
         margin:2rem
     }

</style>