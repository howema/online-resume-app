<template>
  <div class="students-index">
    <div v-for="student in students" :key="student.id">
      <router-link v-bind:to="`/students/${student.id}`">
        <img :src="student.photo_url" alt="no image found" />
        <h2>{{ student.first_name }} {{ student.last_name }}</h2>
        <p>{{ student.bio }}</p>
      </router-link>
    </div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary fixed-top" id="sideNav"></nav>
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
  created: function () {
    this.indexStudents();
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
