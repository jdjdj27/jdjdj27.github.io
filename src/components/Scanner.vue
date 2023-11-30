<template>
  <div class="container">
    <button @click="toggleScan">Scan</button>
    <StreamBarcodeReader
      v-if="isScanning"
      torch
      no-front-cameras
      @decode="onDecode"
      @loaded="onLoaded"
    />
    <h2>Decoded value: {{ scanResult }}</h2>
  </div>
</template>

<script setup>
  import { ref } from 'vue';
  import { StreamBarcodeReader } from '@teckel/vue-barcode-reader';

  const scanResult = ref('');
  const isScanning = ref(false);

  function toggleScan() {
    console.log('-- here');
    isScanning.value = !isScanning.value;
  }

  const onDecode = (result) => {
    console.log('-- result', result);
    isScanning.value = false;
    scanResult.value = result;
  }

  const onLoaded = () => {
    console.log('loaded')
  }
</script>

<style>
  .container {
    display: flex;
    flex-direction: column;
  }
</style>