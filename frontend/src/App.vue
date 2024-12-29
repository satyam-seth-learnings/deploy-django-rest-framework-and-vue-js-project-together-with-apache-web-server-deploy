<template>
  <div class="App">
    <h1>Connect Vue JS to Django</h1>
    <div v-for="(student, index) in students" :key="index">
      <h2>{{ student.stuname }} {{ student.email }}</h2>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  name: "App",
  setup() {
    const students = ref([]);

    const getAllStudents = async () => {
      try {
        const response = await axios.get("http://backend.django-rest-framework-and-vue-js-project.com/api/student/");
        students.value = response.data;
      } catch (error) {
        console.error(error);
      }
    };

    onMounted(() => {
      getAllStudents();
    });

    return {
      students,
    };
  },
};
</script>

<style>
.App {
  text-align: center;
}
</style>
