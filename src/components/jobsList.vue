<template>
    <div>
        <ul>
            <p>{{orderjobSingle}}</p>
            <li v-for="job in orderJobs" :key="job.id">{{job.title}} {{job.location}} {{job.salary}} {{job.title}}</li>
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
        }
    },
    setup(props) {
        const orderJobs = computed(()=> { // computed funkcija izvrsava se kod promene na bilo cemu
            return [...props.jobs].sort((a:Job , b:Job) => {  // tri tacke je da ne mutiramo props vec taj tu array
                return a[props.orderjobSingle] > b[props.orderjobSingle] ? 1 : -1    // ako je a vece dodaj mu jedan a b oduzmi jdan
            })
        })

        return {orderJobs}
    }
})
</script>

<style scoped>

</style>