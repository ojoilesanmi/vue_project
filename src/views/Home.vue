<template>
    
        <AddHealthParameter v-show="showAddHealth" @add-health="addHealth"  />
    
  
    <Health @toggle-reminder="toggleReminder" @delete-health_parameter="deleteHealth" :health_parameters="health_parameters" />
</template>

<script>
import Health from '../components/Health'
import AddHealthParameter from '../components/AddHealthParameter'
export default {
     name: 'Home',
     props: {
        showAddHealth: Boolean,
    },

    components: {
        Health,
        AddHealthParameter,
    },

    data() {
        return {
            health_parameters: [],
        }
    },


    methods: {
   
        async addHealth(health_parameter) {
        const res = await fetch('api/health_parameters', {
            method: 'POST',
            headers: {
            'Content-type': 'application/json',  
            },
            body: JSON.stringify(health_parameter),
        })

        const data = await res.json()


        this.health_parameters = [...this.health_parameters, data]
        },
        async deleteHealth(id){
        if(confirm('Are you sure you want to delete? ')){
            const res = await fetch(`api/health_parameters/${id}`, {
            method: 'DELETE',
            })

            res.status === 200 ? (this.health_parameters = this.health_parameters.filter((health_parameter) => health_parameter.id !== id)) : alert('Error deleting task')
        
        }

        },
        async toggleReminder(id){
        const healthToToggle = await this.fetchHealths(id)
        const updateHealth = {...healthToToggle, reminder:
        !healthToToggle.reminder}

        const res = await fetch(`api/health_parameters/${id}`, {
            method: 'PUT',
            headers: {
            'Content-type': 'application/json'
            },
            body: JSON.stringify(updateHealth)
        }) 

        const data = await res.json()

        this.health_parameters = this.health_parameters.map((health_parameter) => 
        health_parameter.id === id ? {...health_parameter, reminder: !health_parameter.reminder} : health_parameter)
        
        },

        async fetchHealth() {

        const res = await fetch('api/health_parameters')

        const data = await res.json()

        return data


        },

        async fetchHealths(id) {
        const res = await fetch(`api/health_parameters/${id}`)

        const data = await res.json()

        return data
        },

        
        

    },

    async created() {
        this.health_parameters = await this.fetchHealth()
    }
        
}
</script>