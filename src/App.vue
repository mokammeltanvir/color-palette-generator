<template>
  <div id="app">
    <header>
      <h1>Color Palette Generator</h1>
    </header>
    <main>
      <color-picker @color-selected="addColor" />
      <palette-preview :palette="palette" @notify-copied="showCopiedMessage" />
      <button @click="generatePalette">Generate Palette</button>
      <div v-if="copiedMessage" class="popup-message">{{ copiedMessage }}</div>
    </main>
  </div>
</template>

<script>
import ColorPicker from './components/ColorPicker.vue';
import PalettePreview from './components/PalettePreview.vue';

export default {
  components: {
    ColorPicker,
    PalettePreview,
  },
  data() {
    return {
      colors: [],
      palette: [],
      copiedMessage: null,
    };
  },
  methods: {
    addColor(color) {
      this.colors.push(color);
    },
    generatePalette() {
      this.palette = [...this.colors];
    },
    showCopiedMessage() {
      this.copiedMessage = 'Color code copied!';
      setTimeout(() => {
        this.copiedMessage = null;
      }, 1500);
    },
  },
};
</script>

<style>
body {
  font-family: 'Helvetica Neue', sans-serif;
  margin: 0;
  padding: 0;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #1a1a1a;
  color: #fff;
}

header {
  text-align: center;
  padding: 10px 0;
  margin-bottom: 20px;
}

h1 {
  margin: 0;
  font-size: 24px;
}

main {
  background-color: #292929;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin-top: 10px;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s ease;
  margin-left: 5px;
  margin-bottom: 5px;
}

button:hover {
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
