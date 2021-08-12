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
    <div v-for="experience in experiences" :key="experience.id">
      <p>{{ experience.start_date }}</p>
      <p>{{ experience.end_date }}</p>
      <p>{{ experience.job_title }}</p>
      <p>{{ experience.company }}</p>
      <p>{{ experience.details }}</p>
    </div>
    <div v-for="education in educations" :key="education.id">
      <p>{{ education.start_date }}</p>
      <p>{{ education.end_date }}</p>
      <p>{{ education.degree }}</p>
      <p>{{ education.university_name }}</p>
      <p>{{ education.details }}</p>
    </div>
    <div v-for="skill in skills" :key="skill.id">
      <p>{{ skill.name }}</p>
    </div>
    <div v-for="capstone in capstones" :key="capstone.id">
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
      student: {},
      experiences: [],
      educations: [],
      skills: [],
      capstones: [],
    };
  },
  created: function () {
    this.studentShow();
  },
  methods: {
    studentShow: function () {
      axios.get("http://localhost:3000/students" + this.$route.params.id).then((response) => {
        this.student = response.data;
        this.experiences = this.student.experiences;
        this.educations = this.student.educations;
        this.skills = this.student.skills;
        this.capstones = this.student.capstones;
        console.log(response.data);
      });
    },
  },
};
</script>
