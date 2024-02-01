<script setup lang="ts">
import { reactive } from "vue";

class TextPool {
    readonly strs = reactive<string[]>([]);
    constructor() {
    }

    addChar(char: string) {
        const lastStr = this.strs[this.strs.length - 1] || "";
        const newStr = lastStr + char;
        if (newStr.length <= 20) {
            if (this.strs.length === 0) {
                this.strs.push(newStr);
            } else {
                this.strs[this.strs.length - 1] = newStr;
            }
        } else {
            this.strs.push(char);
            if (this.strs.length > 3) {
                this.strs.shift();
            }
        }
    }
}

const textPool = new TextPool();

setInterval(() => {
    textPool.addChar("a" + Math.random().toFixed(2));
}, 500);


</script>

<template>
    <div class="str">
        <span v-for="(text, index) in textPool.strs " :key="text + index" class="block bgc-yellow" >{{ text }}</span>
    </div>
</template>

<style scoped>
.str {
    width: 200px;
    height: 200px;
    transition: transform 0.5s;
}

.str span {
    display: inline-block;
}

.block {
    display: block;
}

.bgc-yellow {
    background-color: yellow;
}
</style>
