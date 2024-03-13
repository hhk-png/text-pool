<script setup lang="ts">
import { reactive, defineProps } from "vue";

interface Props {
  containerWidth?: number;
  containerHeight?: number;
  fontsize?: number;
}

const props = withDefaults(defineProps<Props>(), {
  containerWidth: 600,
  containerHeight: 200,
  fontsize: 20,
})

const {
  containerWidth: WIDTH,
  containerHeight: HEIGHT,
  fontsize: FONTSIZE
} = props


// inner
const PADDING = 5
const NUMOFHORIZONTAL = Math.floor((WIDTH - PADDING * 2) / (FONTSIZE * 0.6))
const NUMOFVERTICAL = Math.floor((HEIGHT - PADDING * 2) / (FONTSIZE * 1.5)) - 1

const strs = reactive<string[]>([])

const addChar = (char: string) => {
  const lastStr = strs[strs.length - 1] || "";
  const newStr = lastStr + char;
  if (newStr.length <= NUMOFHORIZONTAL) {
    if (strs.length === 0) {
      strs.push(newStr);
    } else {
      strs[strs.length - 1] = newStr;
    }
  } else {
    if (strs.length > NUMOFVERTICAL) {
      strs.shift()
    }
    strs.push(char)
  }
}

const strStyle = {
  width: WIDTH + "px",
  height: HEIGHT + "px",
  padding: PADDING + "px",
  fontSize: FONTSIZE + "px",
};

defineExpose({ addChar })


</script>

<template>
  <div :style="strStyle" class="str">
    <span v-for="(text, index) in strs" :key="text + index" class="bgc-yellow">{{ text }}</span>
  </div>
</template>

<style scoped>
.str {
  background-color: antiquewhite;
  box-sizing: border-box;
}

.str span {
  display: inline-block;
}

.bgc-yellow {
  background-color: yellow;
}
</style>
