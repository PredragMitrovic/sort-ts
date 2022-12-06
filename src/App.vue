<template>
  <div>
    
    <button @click="clickOrderJobList('salary')">Orrder by salary</button>
    <button @click="clickOrderJobList('title')">Orrder by title</button>
    <button @click="clickOrderJobList('location')">Orrder by location</button>
    <input type="text" v-model="searchByTitle">
    <p>{{searchByTitle}}</p>
    <job-list :jobs='jobs'  :orderjobSingle = 'orderjobSingle' :searchByTitle='searchByTitle'/>
    <button @click="tsComponentShow =! tsComponentShow">Pokazi TS komponentu</button>
    <hr>
    <div v-if="tsComponentShow">
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

    const jobs = ref<Job[]>([
      {title: 'programer' , location: 'Zemun', salary: 1000, id: 1},
      {title: 'masinovodja' , location: 'Beeograd', salary: 2000, id: 12},
      {title: 'bokser' , location: 'Novi sad', salary: 7000, id: 13},
      {title: 'zigolo' , location: 'Arandjelovac', salary: 6000, id: 14},
      {title: 'fudbaler' , location: 'Kopaonik', salary: 4000, id: 15},
      {title: 'peruanac' , location: 'Minhen', salary: 3000, id: 16},
    ])
    const orderjobSingle = ref<JobOrder>('title')

    const clickOrderJobList = (jobOrderParametter: JobOrder) => {
      orderjobSingle.value = jobOrderParametter 
    }
    // filter 
     const searchByTitle = ref('')

    return { jobs, orderjobSingle, clickOrderJobList, searchByTitle  } // 3 tacke da razdvoji na individualne propertije unutar objekta
  }
});
</script>

<style>

</style>
