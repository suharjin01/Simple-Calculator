<script setup lang="ts">
import { invoke } from "@tauri-apps/api/core";

</script>
<script lang="ts">

export default {
  data() {
    return {
      num1: 0,
      num2: 0,
      operation: "add",
      result: null,
      error: null,
    };
  },
  methods: {
    async calculate() {
      try {
        this.error = null;
        this.result = await invoke("calculate", {
          operation: this.operation,
          a: this.num1,
          b: this.num2,
        });
      } catch (e) {
        this.error = e.message || "Terjadi kesalahan.";
      }
    },
  },
};
</script>

<template>
  <div id="app">
    <h1>Kalkulator Sederhana</h1>
    <input type="number" v-model.number="num1" placeholder="Angka 1" />
    <select v-model="operation">
      <option value="add">Tambah</option>
      <option value="subtract">Kurangi</option>
      <option value="multiply">Kali</option>
      <option value="divide">Bagi</option>
    </select>
    <input type="number" v-model.number="num2" placeholder="Angka 2" />
    <button @click="calculate">Hitung</button>
    <p>Hasil: {{ result }}</p>
    <p v-if="error" style="color: red;">Error: {{ error }}</p>
  </div>
</template>

<style>
#app {
  text-align: center;
  margin-top: 50px;
}
input, select {
  margin: 10px;
}
</style>