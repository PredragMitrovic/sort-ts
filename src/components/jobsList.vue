<template>
    <div>
        <ul>
            <li v-for="job in filterJobs" :key="job.id">{{job.title}} {{job.location}} {{job.salary}}</li>
        </ul>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import OrderJob from '../types/jobOrder'
import Job from './../types/job'

export default defineComponent({

    props: {
        jobs: {
            required: true,
            type: Array as PropType<Job[]>
        },
        orderjobSingle: {
            required: true, 
            type: String as PropType<OrderJob>
        },
        searchByTitle: {
            required: true,
            type: String
        }
    },
    setup(props) {
        // prvo sam napravio sort funkciju da bi bilo jasnije i posle sam samo sort dodao u filter funkciju da bi bilo na istom mestu
        const orderJobs = computed(() => { // computed funkcija izvrsava se kod promene na bilo cemu
            return [...props.jobs].sort((a:Job , b:Job) => {  // tri tacke je da ne mutiramo props vec taj tu array
                return a[props.orderjobSingle] > b[props.orderjobSingle] ? 1 : -1    // ako je a vece dodaj mu jedan a b oduzmi jdan
            })
        })

        const filterJobs = computed(() => {
            return [...props.jobs].filter((jobs) => jobs.title.includes(props.searchByTitle) )
            .sort((a:Job , b:Job) => {  
                return a[props.orderjobSingle] > b[props.orderjobSingle] ? 1 : -1    
            })
        })
        return {orderJobs, filterJobs }
    }
})
</script>

<style scoped>

</style>