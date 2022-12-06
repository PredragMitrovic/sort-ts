<template>
<div>
    <div>
        <h1>TS komponenta</h1>
        <hr>
        <div>
            <button @click="changeName('Zika')">Promeni ime</button>
            <p>{{ime}}</p>
        </div>
        <hr>
        <div>
            <button @click="changeAge('77 fddf')">Promeni godinu</button>
            <p>{{godina}}</p>
        </div>
    </div>
</div>

</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    data() {
        return {
            ime: 'Pera', // nee mora da se definise tajp, odmah ga zna da je string
            godina:  25 as number | string // ovako kazemod a moze da bude i jedno i drugo
        }
    },
    methods: {
        changeName(nekoIme: string) { // parametar mora da se definise tajp
            this.ime = nekoIme
        },
        changeAge(someYears: number | string) {  // takodje moze biti samo string ili samo number jer je tako definisano u dati
            this.godina = someYears
        }
    }
})
</script>
