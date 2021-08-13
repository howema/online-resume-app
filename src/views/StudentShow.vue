<template>
  <div class="students-show">
    <!-- Navigation-->
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary fixed-top" id="sideNav">
      <a class="navbar-brand js-scroll-trigger" href="#page-top">
        <span class="d-block d-lg-none"></span>
        <span class="d-none d-lg-block">
          <img class="img-fluid img-profile rounded-circle mx-auto mb-2" :src="student.photo_url" alt="..." />
        </span>
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarResponsive"
        aria-controls="navbarResponsive"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarResponsive">
        <ul class="navbar-nav">
          <li class="nav-item"><a class="nav-link js-scroll-trigger" href="#about">About</a></li>
          <li class="nav-item"><a class="nav-link js-scroll-trigger" href="#experience">Experience</a></li>
          <li class="nav-item"><a class="nav-link js-scroll-trigger" href="#education">Education</a></li>
          <li class="nav-item"><a class="nav-link js-scroll-trigger" href="#skills">Skills</a></li>
          <li class="nav-item"><a class="nav-link js-scroll-trigger" href="#interests">Interests</a></li>
          <li class="nav-item"><a class="nav-link js-scroll-trigger" href="#awards">Awards</a></li>
        </ul>
      </div>
    </nav>
    <!-- Page Content-->
    <div class="container-fluid p-0">
      <!-- About-->
      <section class="resume-section" id="about">
        <div class="resume-section-content">
          <h1 class="mb-0">
            {{ student.first_name }}
            <span class="text-primary">{{ student.last_name }}</span>
          </h1>
          <div class="subheading mb-5">
            {{ student.phone_number }} ·
            <a href="`mailto:${student.email}`">{{ student.email }}</a>
          </div>
          <p class="lead mb-5">{{ student.bio }}</p>
          <div class="social-icons">
            <a class="social-icon" href="`${student.linkedin_url}`"><i class="fab fa-linkedin-in"></i></a>
            <a class="social-icon" href="`${student.github_url}`"><i class="fab fa-github"></i></a>
            <a class="social-icon" href="`${student.twitter_handle}`"><i class="fab fa-twitter"></i></a>
            <a class="social-icon" href="`${student.website}`"><i class="fab fa-facebook-f"></i></a>
          </div>
        </div>
      </section>
      <hr class="m-0" />
    </div>
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
      axios.get("http://localhost:3000/students/" + this.$route.params.id).then((response) => {
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
