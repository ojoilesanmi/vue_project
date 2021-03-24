<template>
    <div @dblclick="$emit('toggle-reminder', health_parameter.id)" :class="[health_parameter.reminder ? 'reminder' : '', 'task']">

        <h3> {{ health_parameter.text }}</h3>
            <i @click="$emit('delete-health_parameter', health_parameter.id)"  class="fas fa-times"></i>
        <p> {{ health_parameter.when }}</p>
    </div>
    
</template>

<script>

export default {
    name: 'Healths',
    props: {
        health_parameter: Object
    },
   
}
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>