<template>
  
<div class="box">
    <div class="person--container">
      <h3>Lista zawodników oraz składek</h3>
      <input class=" inputField" type="text" placeholder="Imię" v-model="newName">
      <input class=" inputFieldNum" type="number" placholder="0" v-model="newAmount">
<!--       ID <input class=" inputFieldNum" type="number" placholder="id" v-model="newId"> -->
      <button @click="addPerson">Dodaj</button>

      <personCom
          v-for="person in persons" 
          v-bind:key="person.id" 
          :person="person"
          @personPaidFee = 'personPaid'/>
        
          <p>
            Suma: 
          </p><p id="wynik" onload="countAmount"></p> <button @click="countAmount">Wyświetl sume</button>
    </div>

        <div class="person--container">
          <h3>Lista wydatków</h3>
          <input class=" inputField" type="text" placeholder="Nazwa" v-model="newName">
          <input class=" inputFieldNum" type="number" placholder="0" v-model="newAmount">
          ID <input class=" inputFieldNum" type="number" placholder="id" v-model="newId">
          <button @click="addPerson">Dodaj</button>
      
        </div>
</div>
</template>

<script>
import personCom from './PersonPlayer.vue'
export default {
    components:{
        personCom
    },
  data() {
    return {
      newName: '',
      newAmount: 0,
      newId: '',
      persons: [
        { name: 'Albert', amount: 0, id: 1, paidAmount: false },
        { name: 'Marcin', amount: 40, id: 2, paidAmount: false },
        { name: 'Kuba', amount: 50, id: 3, paidAmount: true },
      ]
    }
  },
  methods: {
    addPerson() {
      let testID= this.persons.length + 1;
      console.log(testID);
      this.persons.push({
        name: this.newName,
        amount: this.newAmount,
        id: testID,
        paidAmount:false,
      })
      this.newName = ''
    },
    updateAmount(id, amount) {
      const index = this.persons.findIndex(el => el.id === id)
      console.log(index)
      console.log(amount)
      /*      this.persons[index].amount += amount  */
    },
    personPaid(id) {
      const index = this.persons.findIndex(el => el.id === id)
      console.log(index)
/*       this.persons[index].paid == 50 */
      this.persons[index].paidAmount = true
    },
    countAmount(){

      let suma = 0;
      
      for(let i=0;i<this.persons.length;i++){
      suma+=this.persons[i].amount;
      }
      document.getElementById('wynik').innerHTML = suma;
      
      return suma;
    },
  }
}
</script>

<style>

.box{
  display: flex;
  justify-content: center;
}
.app--container {
  border: dotted 2px black;
  text-align: center;
  width: 88vw;
}

h2 {
  text-align: center;
}

h3 {
  text-align: center;
}

.person--container {
  border: solid 2px black;
  margin: 4px;
  padding: 6px;
  width: 40vw;
}

.inputField {
  width: 15vw;
}

.inputFieldNum {
  width: 4vw;
}

.person {
  border: solid 1px black;
  margin: 6px;
  padding: 4px;
}

.person p {
  font-size: 1em;
}

.paid {
  opacity: 0.5;
  text-decoration: line-through;
}
</style>