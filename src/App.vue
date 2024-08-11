<script setup>
import { computed, ref, watch } from "vue";
import { useClipboard, useTitle } from "@vueuse/core";
import pangu from "pangu";

useTitle(`pangu ${pangu.version}`);

const text = ref("");
const source = computed(() => pangu.spacing(text.value) || "N/A");

const { copy, copied } = useClipboard({ source });

async function runExample() {
  text.value = `如果你跟我一樣，每次看到網頁上的中文字和英文、數字、符號擠在一塊，就會坐立難安，忍不住想在它們之間加個空格。這個外掛（支援Chrome和Firefox）正是你在網路世界走跳所需要的東西，它會自動替你在網頁中所有的中文字和半形的英文、數字、符號之間插入空白。

漢學家稱這個空白字元為「盤古之白」，因為它劈開了全形字和半形字之間的混沌。另有研究顯示，打字的時候不喜歡在中文和英文之間加空格的人，感情路都走得很辛苦，有七成的比例會在 34 歲的時候跟自己不愛的人結婚，而其餘三成的人最後只能把遺產留給自己的貓。畢竟愛情跟書寫都需要適時地留白。

與大家共勉之。`;
}
</script>

<template>
  <h1>pangu {{ pangu.version }}</h1>
  <p>
    powered by
    <a
      href="https://github.com/vinta/pangu.js"
      target="_blank"
      rel="noreferrer noopener"
      >vinta/pangu.js</a
    >
  </p>
  <p><a href="#" @click.prevent="runExample()">run example</a></p>
  <textarea v-model="text" />
  <p>result</p>
  <pre><code class="transformed">{{ source }}</code></pre>
  <div v-if="text">
    <a href="#" @click.prevent="copy()">copy to clipboard</a>
    <span class="copied" v-if="copied">done!</span>
  </div>
  <p>
    css
    <a
      href="https://watercss.kognise.dev/"
      target="_blank"
      rel="noreferrer noopener"
    >
      water.css
    </a>
  </p>
</template>

<style scoped>
.copied {
  margin-left: 0.5rem;
}

.transformed {
  text-wrap: wrap;
}
</style>
