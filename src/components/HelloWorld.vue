<template>
  
  <form>
    <label for="studentName">Student name</label>
    <input type="text" id="studentName" name="studentName" v-model="studentName" />

    <label for="studentEmail">Student email</label>
    <input type="text" id="studentEmail" name="studentEmail" v-model="studentEmail" />

    <label for="birthDate">Date of birth</label>
    <input type="date" id="birthDate" name="birthDate" v-model="birthDate" />

    <button @click="submitHandler">Upload student</button>
  </form>

  <div>
    <h4>Update student list</h4>

    <button @click="getStudentHandler">refresh</button>
  </div>



</template>

<script setup lang="ts">
import { ref } from 'vue'

import axios from 'axios'

defineProps<{ msg: string }>()

const submitHandler = async (e: Event) => {

  e.preventDefault();
  console.log("se subio el forms");

  console.log('asi esta la fecha',birthDate.value)

  // make post request
  axios.post("http://localhost:8080/api/v1/student", {
     name: studentName.value,
     email: studentEmail.value,
     dob: birthDate.value

   })

}

const getStudentHandler = async (e: Event) => {

  const studentList = axios.get('http://localhost:8080/api/v1/student')

  console.log('grupo de students:', studentList)

  studentsObj.value = studentList;

}

const count = ref(0)
const studentName = ref('')
const studentEmail = ref('')
const birthDate = ref('')

const studentsObj = ref({})

</script>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
