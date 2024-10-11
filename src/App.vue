<script setup>
import { ref, computed } from 'vue';

// カウントや選択値のリアクティブなデータ
const count = ref(0);
const selectedProbability = ref(512);

// 確率の計算をリアクティブに実行
const probability = computed(() => {
  const prob = 1 - (((selectedProbability.value - 1) / selectedProbability.value) ** count.value);
  return (prob * 100).toFixed(5);
});

// カウントを増減する関数
const increment = () => count.value++;
const decrement = () => count.value > 0 && count.value--;
const reset = () => count.value = 0;
</script>

<template>
<div class="bod">
<h1>色違いトリガー</h1>
  <div class="container">
    <div class="field">
      <button class="button" @click="decrement">－</button>
      <input type="text" :value="count" class="inputtext" readonly />
      <button class="button" @click="increment">＋</button>
    </div>
    <button class="button resetbtn" @click="reset">RESET</button>
  </div>

  <div class="Shiny_Probability">
    <label>色違い確率：
      <select v-model="selectedProbability">
        <option value="512">1/512</option>
        <option value="1024">1/1024</option>
        <option value="4096">1/4096</option>
        <option value="8192">1/8192</option>
      </select>
    </label>        
        
    <div class="prob-display">
      <p>{{ count }}回までに色違いが出る確率:</p>
      <p>{{ probability }}%</p>
    </div>
  </div>
  </div>
</template>

<style scoped>
h1{
  color:white;
}
.bod {
  width: 100%;
  background-color:black;
}

.container {
  width: 250px;
  margin: 200px auto;
}

.field {
  display: flex;
}

.inputtext {
  color: rgba(43, 32, 32, 0.76);
  font-size: 18px;
  border-left: 0;
  border-right: 0;
  width: 80px;
  line-height: 3rem;
  text-align: center;
  border: 1px solid #D7DBDD;
  padding: 0 10px;
}

.button {
  color: rgba(43, 32, 32, 0.76);
  font-size: 18px;
  cursor: pointer;
  padding: 5px 25px;
  background-color: white;
  border: 1px solid #D7DBDD;
  border-radius: 0;
  outline: 0;
}

.resetbtn {
  margin: 20px 0 0 65px;
}

.Shiny_Probability {
  padding: 10px;
  margin: -100px auto;
  width: 250px;
  border: 1px solid #858585;
  border-radius: 10px;
}

#prob-list {
  margin: 0 auto;
}
</style>
