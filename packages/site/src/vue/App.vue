<script setup>
import { onMounted, ref, watch } from 'vue'
import HighlightableInput from 'highlightable-input/vue'
import { tweet } from '../rules'

const text = ref('Hello Mayor @Goodway!')
const vueTheme = ref('none')

const multiline = ref(false)
const readonly = ref(false)
const disabled = ref(false)
const setHighlight = ref(false)

const tweetrule = ref()
tweetrule.value = tweet
console.log('1 ui set highlight:',tweetrule.value,tweet)

watch(readonly, (value) => {
  if (value) {
    disabled.value = false
  }
})

watch(disabled, (value) => {
  if (value) {
    readonly.value = false
  }
})

watch(setHighlight, (value) => {
  if (value) {
    tweetrule.value =  tweet
  //   tweetrule.value =   {
  //   pattern: new RegExp('你好|关键字|鼠标', 'gi'),
  //   class: 'link'
  // };
    console.log('2 ui set highlight:',tweetrule.value,tweet)
  } else {
    tweetrule.value = []
  }
    
})
    
onMounted(() => {
  window.registerVueApp((theme) => {
    vueTheme.value = theme
  })
})
</script>

<template>
  <h2><label for="vue">Vue App</label><img src="/vue.svg" height="16" /></h2>
  <section class="settings">
    <label><input type="checkbox" v-model="multiline" />Multiline</label>
    <label><input type="checkbox" v-model="readonly" />Readonly</label>
    <label><input type="checkbox" v-model="disabled" />Disabled</label>
    <label><input type="checkbox" v-model="setHighlight" />setHighlight</label>
  </section>
  <HighlightableInput
    id="vue"
    :theme="vueTheme"
    v-model="text"
    :highlight="tweetrule"
    :multiline="multiline"
    :readonly="readonly"
    :disabled="disabled"
  />
</template>
