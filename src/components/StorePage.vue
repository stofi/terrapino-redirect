<template>
    <div class="card pa-8 mx-auto mt-12 max-width" flat>
        <div class="text-center mb-6">
            <h2>{{ storeTitle }}</h2>
        </div>

        <div class="d-flex  justify-center">
            <button color="#00228A" dark elevation="0" large depressed @click="redirect">{{ redirectButtonText }}</button>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { computed, onMounted, ref } from 'vue';


const cs = {
    'store.titleApple': 'Otevřít aplikaci v App Store',
    'store.titleAndroid': 'Otevřít aplikaci v Play Store',
    'store.redirectButtonText': 'Otevřít',
}

const en: typeof cs = {
    'store.titleApple': 'Open app in App Store',
    'store.titleAndroid': 'Open app in Play Store',
    'store.redirectButtonText': 'Open',
}

const locale = ref<'cs' | 'en'>('en')

const setLocale = (newLocale: 'cs' | 'en') => {
    locale.value = newLocale
}

const $t = (key: keyof typeof cs) => {
    return locale.value === 'cs' ? cs[key] : en[key]
}
const storeTitle = computed(() => {
    const userAgent = window.navigator.userAgent.toLowerCase()
    const isIos = /iphone|ipad|ipod/.test(userAgent)
    return isIos ? $t('store.titleApple') : $t('store.titleAndroid')
})
const redirectButtonText = computed(() => {
    return $t('store.redirectButtonText')
})
const link = ref('')


onMounted(() => {
    if (isIos()) {
        link.value = 'https://apps.apple.com/cz/app/terrapino/id1660281404'
    } else if (isAndroid()) {
        link.value =
            'https://play.google.com/store/apps/details?id=cz.alzheimerchain.terrapino'
    } else {
        link.value = ''
    }
    if (link.value) window.location.href = link.value

    const culture = navigator.language.match(/cs/) ? 'cs-CZ' : 'en-US'
    setLocale(culture === 'cs-CZ' ? 'cs' : 'en')

    console.log('locale', locale.value)
})

function redirect() {
    if(!link.value) return
    window.location.href = link.value
}

function isIos(): boolean {
    const userAgent = window.navigator.userAgent.toLowerCase()
    return /iphone|ipad|ipod/.test(userAgent)
}

function isAndroid(): boolean {
    const userAgent = window.navigator.userAgent.toLowerCase()
    return /android/.test(userAgent)
}

</script>

<style scoped>
.pa-8 {
    padding: 2rem;
}

.mt-12 {
    margin-top: 3rem;
}

.mx-auto {
    margin-left: auto;
    margin-right: auto;
}

.justify-center {
    justify-content: center;
}

.text-center {
    text-align: center;
}

.mb-6 {
    margin-bottom: 1.5rem;
}

.max-width {
    max-width: min(100%, 500px);
}

.d-flex {
    display: flex;
}

.card {
    background: #fff;
    border-radius: .5rem;
    width: 100%;
}

button {
    border-radius: .5rem;
    border: 0;
    color: #fff;
    background: rgb(0, 34, 138) none no-repeat scroll 0% 0% / auto padding-box border-box;
    padding: 1rem 1rem;
    text-transform: uppercase;
    letter-spacing: 1.25px;
    font-size: .8rem;
    font-weight: 500;
}

h2 {
    background: rgba(0, 0, 0, 0) none no-repeat scroll 0% 0% / auto padding-box border-box;
    box-sizing: border-box;
    color: rgba(0, 0, 0, 0.87);
    display: block;
    font: 700 24px / 36px Roboto, sans-serif;
    height: 36px;
    margin: 0px;
    margin-block: 0px;
    margin-inline: 0px;
    overflow-wrap: break-word;
    padding: 0px;
    tab-size: 4;
    text-align: center;
    text-rendering: optimizelegibility;
    white-space: normal;
    width: 436px;
    word-break: normal;
    -webkit-font-smoothing: antialiased;
}</style>