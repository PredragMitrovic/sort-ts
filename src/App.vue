<template>
  <div>
    
    <button @click="clickOrderJobList('salary')">Orrder by salary</button>
    <button @click="clickOrderJobList('title')">Orrder by title</button>
    <button @click="clickOrderJobList('location')">Orrder by location</button>
    <job-list :jobs='jobs'  :orderjobSingle = 'orderjobSingle'/>

    <button @click="tsComponentShow =! tsComponentShow">Pokazi TS komponentu</button>
    <hr>
    <div v-if="tsComponentShow">
      <p>{{nesto}}</p>
      <hr>
      <tsComponent/>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from 'vue';
import tsComponent from './components/tsType.vue'
import jobList from './components/jobsList.vue'
import Job from './types/job'
import JobOrder from './types/jobOrder'

export default defineComponent({
  name: 'App',
  components: {
    tsComponent,
    jobList
  },
  data() {
    return {
      tsComponentShow: false,
    }
  },
  setup() {
    const state = reactive({
      mojeIme: 'Peki majstorcina',
      mojeGodiste: 1983 as string | number
    })
    const nesto = ref<number | string>(123)

    const jobs = ref<Job[]>([
      {title: 'programer' , location: 'Zemun', salary: 2500, id: 1},
      {title: 'programer2' , location: 'Zemun2', salary: 25200, id: 12},
      {title: 'programer3' , location: 'Zemun3', salary: 25030, id: 13},
      {title: 'programer44' , location: 'Zemun4', salary: 25400, id: 14},
      {title: 'programer5' , location: 'Zemun5', salary: 25500, id: 15},
      {title: 'programer6' , location: 'Zemu6n', salary: 25006, id: 16},
    ])
    const orderjobSingle = ref<JobOrder>('title')

    const clickOrderJobList = (jobOrderParametter: JobOrder) => {
      orderjobSingle.value = jobOrderParametter 
    }

    return { ...toRefs(state), nesto, jobs, orderjobSingle, clickOrderJobList  } // 3 tacke da razdvoji na individualne propertije unutar objekta
  },
  methods: {
    changeIme (parametar: string) {
      this.mojeIme = parametar
      return parametar
    }
  }
});
</script>

<style>

</style>
