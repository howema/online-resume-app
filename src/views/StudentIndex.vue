<template>
  <div class="students-index">
    <div v-for="student in students" :key="student.id">
      <router-link v-bind:to="`/students/${student.id}`">
        <img :src="student.photo" alt="no image found" />
        <h2>{{ student.first_name }} {{ student.last_name }}</h2>
        <p>{{ student.short_bio }}</p>
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      students: [],
    };
  },
  methods: {
    indexStudents: function () {
      axios.get("http://localhost:3000/students").then((response) => {
        this.students = response.data;
        console.log("all students", this.students);
      });
    },
  },
};
</script>
