<template>
    <div class="color-picker">
      <input type="color" v-model="selectedColor" @input="updatePalette" />
      <button @click="copyColor">Copy</button>
      <div v-if="copied" class="popup-message">Color code copied!</div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        selectedColor: '#ffffff',
        copied: false,
      };
    },
    methods: {
      updatePalette() {
        this.$emit('color-selected', this.selectedColor);
      },
      copyColor() {
        const input = document.createElement('input');
        input.value = this.selectedColor;
        document.body.appendChild(input);
        input.select();
        document.execCommand('copy');
        document.body.removeChild(input);
  
        this.copied = true;
        setTimeout(() => {
          this.copied = false;
        }, 1500);
      },
    },
  };
  </script>
  
  <style scoped>
  .color-picker {
    display: flex;
    align-items: center;
    margin: 10px;
  }
  
  .color-picker button {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s ease;
  }
  
  .color-picker button:hover {
    background-color: #0056b3;
  }
  
  .popup-message {
    background-color: rgba(0, 0, 0, 0.7);
    color: #fff;
    padding: 5px 10px;
    border-radius: 5px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 1000;
  }
  </style>
  