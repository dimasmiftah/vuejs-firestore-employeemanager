<template>
    <div id="dashboard">
        <ul class="collection with-header">

            <li class="collection-header">
                <h4>Employees</h4>
            </li>

            <li class="collection-item" v-for="employee in employees" :key="employee.id">
                <div class="chip">{{employee.dept}}</div>
                {{employee.employee_id}} : {{employee.name}}
                
                <router-link v-bind:to="{name:'view-employee', params: {employee_id: employee.employee_id}}" class="secondary-content">
                    <li class="fa fa-eye"></li>
                </router-link>
            </li>
        </ul>

        <div class="fixed-action-btn">
            <router-link to="/new" class="btn-floating btn-large red">
                <i class="fa fa-plus"></i>
            </router-link>
        </div>
    </div>
</template>
<script>
import db from './firebaseInit.js'
export default {
    name: 'dashboard',
    data(){
        return {
            employees: []
        }
    },
    created() {
        db.collection('employees').orderBy('dept').get().then
        (querySnapshot => {
            querySnapshot.forEach(doc => {
                const data = {
                    'id' : doc.id,
                    'employee_id' : doc.data().employee_id,
                    'name' : doc.data().name,
                    'dept' : doc.data().dept
                }
                this.employees.push(data);
                console.log(this.employees);
                
            });
        })
    },
}
</script>
<style>

</style>


