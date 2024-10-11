<script setup>
import { ref, computed } from 'vue';

// カウントや選択値のリアクティブなデータ
const count = ref(0);
const selectedProbability = ref(512);

// 確率の計算をリアクティブに実行
const probability = computed(() => 
  ((1 - Math.pow((selectedProbability.value - 1) / selectedProbability.value, count.value)) * 100).toFixed(5)
);

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
h1 {
  color:white;
  position: relative;
  padding-left: 25px;
}

h1:before {
  position: absolute;
  content: '';
  bottom: -3px;
  left: 0;
  width: 0;
  height: 0;
  border: none;
  border-left: solid 15px transparent;
  border-bottom: solid 15px rgb(119, 195, 223);
}
h1:after {
  position: absolute;
  content: '';
  bottom: -3px;
  left: 10px;
  width: 100%;
  border-bottom: solid 3px rgb(119, 195, 223);
}
.bod {
  width: 100%;
  background-color:#30313d;
}

.container {
  width: 250px;
  margin: 200px auto;
}

.field {
  display: flex;
  background-color: white;
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
  font-size: 18px;
  cursor: pointer;
  padding: 5px 25px;
  border: 1px solid #D7DBDD;
  border-radius: 0;
  outline: 0;
}

.resetbtn {
  margin: 20px 0 0 65px;
  background-color: #515266;
  border: 1px solid #ff5722;
  border-radius: 2px;
  color: #ff5722;
}

.Shiny_Probability {
  padding: 10px;
  margin: -150px auto;
  width: 250px;
  border: 1px solid #858585;
  border-radius: 5px;
  background-color: white;
}

#prob-list {
  margin: 0 auto;
}
</style>
