<template>
    <div :key="health_parameter.id" v-for="health_parameter in health_parameters">
        <Healths @toggle-reminder="$emit('toggle-reminder', health_parameter.id)" @delete-health_parameter="$emit('delete-health_parameter', health_parameter.id)" :health_parameter="health_parameter" /> 
    </div>
</template>

<script>
import Healths from './Healths'
export default {
    name: 'Health',
    props: {
        health_parameters: Array,
    },
    components: {
       Healths 
    },
    emits: ['delete-health_parameter', 'toggle-reminder'],
}
</script>