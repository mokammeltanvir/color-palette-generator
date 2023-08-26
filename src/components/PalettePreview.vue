<template>
    <div class="palette-preview">
      <div
        v-for="(color, index) in palette"
        :key="index"
        class="color-swatch"
        :style="{ backgroundColor: color }"
        @click="copyColor(color)"
      >
        {{ color }}
        <div v-if="copied" class="popup-message">Code copied!</div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      palette: Array,
    },
    data() {
      return {
        copied: false,
      };
    },
    methods: {
      copyColor(color) {
        const input = document.createElement('input');
        input.value = color;
        document.body.appendChild(input);
        input.select();
        document.execCommand('copy');
        document.body.removeChild(input);
  
        this.copied = true;
        setTimeout(() => {
          this.copied = false;
        }, 1500);
  
        this.$emit('notify-copied');
      },
    },
  };
  </script>
  
  <style scoped>
  .palette-preview {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin: 20px;
  }
  
  .color-swatch {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 80px;
    height: 80px;
    margin: 5px;
    border-radius: 50%;
    cursor: pointer;
    transition: background-color 0.3s ease;
    position: relative;
  }
  
  .color-swatch:hover {
    background-color: rgba(0, 0, 0, 0.1);
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
    z-index: 1;
    display: none;
  }
  
  .color-swatch:hover .popup-message {
    display: block;
  }
  </style>
  