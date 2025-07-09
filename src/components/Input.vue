<template>
  <input min="0" type="number" @input="this.changeAmount($event.target.value)" />
  <button class="light-blue-button" @click="convert()">Convert</button>
  <button class="light-blue-button" @click="favourite()">Add to favourites</button>
</template>

<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true
    },
    convert: {
      type: Function,
      required: true
    },
    favourite: {
      type: Function,
      required: true
    }
  },

  
};
</script>

<style scoped>
input {
  width: 500px;
  font-size: 1.2em;
  border-radius: 3px;
  border: 0;
  padding: 10px 15px;
  background: #fafafa;
  color: #333;
  outline: none;
}
.light-blue-button {
  margin: 0 10px;
  background-color: #1e91c6;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.light-blue-button:hover {
  background-color: #166a92; /* Slightly darker on hover */
  transform: translateY(-2px);
}

.light-blue-button:active {
  background-color: #4996c0;
  transform: translateY(0);
}

</style>
