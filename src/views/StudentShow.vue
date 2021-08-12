<template>
  <div class="students-show">
    <div>
      <img :src="student.photo_url" alt="no image found" />
      <h2>{{ student.first_name }} {{ student.last_name }}</h2>
      <p>{{ student.bio }}</p>
      <p>{{ student.email }}</p>
      <p>{{ student.phone_number }}</p>
      <p>{{ student.linkedin_url }}</p>
      <p>{{ student.twitter_handle }}</p>
      <p>{{ student.website }}</p>
      <p>{{ student.github_url }}</p>
    </div>
    <div v-for="experience in experiences">
      <p>{{ experience.start_date }}</p>
      <p>{{ experience.end_date }}</p>
      <p>{{ experience.job_title }}</p>
      <p>{{ experience.company }}</p>
      <p>{{ experience.details }}</p>
    </div>
    <div v-for="education in educations">
      <p>{{ education.start_date }}</p>
      <p>{{ education.end_date }}</p>
      <p>{{ education.degree }}</p>
      <p>{{ education.university_name }}</p>
      <p>{{ education.details }}</p>
    </div>
    <div v-for="skill in skills">
      <p>{{ skill.name }}</p>
    </div>
    <div v-for="capstone in capstones">
      <p>{{ capstone.name }}</p>
      <p>{{ capstone.description }}</p>
      <p>{{ capstone.url }}</p>
      <img :src="capstone.screenshot" />
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
