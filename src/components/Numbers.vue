<template>
  <div>
    <div class="number" :id="'number-'+number" v-for="number in numbersList()" :key="number" @mouseover="numbersHover(number)" @mouseout="reset">
      {{number}}
    </div>
  </div>
</template>

<script>
export default {
  data()
  {
    return {
      limit: this.$parent.limit,
      numbers: [],
      // Created a variable that can be used by multiple methods. 
      // This way, the same variable does not need to be created twice.
      // The variable is used to store all elements with the class name ".number".
      allNumbers: null
    }
  },
  watch: {
    ['$parent.limit'](newLimit)
    {
      this.limit = newLimit;
    }
  },
  methods: {
    // An array shuffle function using the Fisher-Yates algorithm.
    // This algorithm provides a better, more randomized and faster shuffle than sort()
    shuffleArray(array) {
      let receivedArray = array;
      for (let i = receivedArray.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [receivedArray[i], receivedArray[j]] = [receivedArray[j], receivedArray[i]];
      }
      return receivedArray;
    },

    // Change the name of the function to something that is clearer to understand, as per JavaScript's best practices.
    // From n() -> To numbersList()
    numbersList()
    {
      let numbers = [];

      // As per the requirements, the application must display values from 1 to 100 (100 the number inputted)
      // Therefore, the variable "i" starts from 1 (not from 0 as initially set) and increments until 
      // the last value (limit) on the input, by using "<=" instead of "<".
      // The same could be achieved by doing i=1 and i < this.limit + 1.
      for(var i = 1; i <= this.limit; i++)
        // For preference reasons; numbers = [...numbers, i] is exactly the same as numbers.push(i) with more code.
        numbers.push(i);
        
      return this.shuffleArray(numbers);
    },
    // Change the name of the function to something that is clearer to understand, as per JavaScript's best practices.
    // From hov() -> To numbersHover()
    numbersHover(number)
    {
      // Assigning all elements with class="number" to the variable allNumbers as set and returned on the data() method.
      this.allNumbers = document.querySelectorAll('.number');

      for(let i = 0; i < this.allNumbers.length; i++)
      {
        // The textContent of all the elements returns a string but it is used as a Number.
        // Therefore, it has been converted to a valid number by using the parseInt() method.
        // The .trim() method has been left as it is an additional check for the number validation proccess.
        // Extra: The same can be done with the "+" symbol (e.g. +myValue.trim()) or Number() method, as well as other methods.
        const num = parseInt(this.allNumbers[i].textContent.trim());
        if(number % num === 0) this.allNumbers[i].classList.add('active')
      }
    },
    reset()
    {
      // Since the reset() method is called after the numbersHover() 
      // we can assume that the variable allNumbers will have already been set,
      // thus, we do not need to assign all the elements with class="number" to it again.
      this.allNumbers.forEach(num => num.classList.remove('active'))
    }
  }
}
</script>

<style scoped>
	.number {
		display: inline-block;
		padding: 5px;
		background-color: lightgrey;
		margin: 5px;
	}

	.active {
		background-color: red;
	}
</style>
