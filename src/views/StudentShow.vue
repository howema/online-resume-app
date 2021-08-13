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
          <li class="nav-item"><a class="nav-link js-scroll-trigger" href="#capstones">Capstones</a></li>
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
      <!-- Experience-->
      <section class="resume-section" id="experience">
        <div class="resume-section-content">
          <h2 class="mb-5">Experience</h2>
          <div v-for="experience in experiences" :key="experience.id">
            <div class="d-flex flex-column flex-md-row justify-content-between mb-5">
              <div class="flex-grow-1">
                <h3 class="mb-0">{{ experience.job_title }}</h3>
                <div class="subheading mb-3">{{ experience.company }}</div>
                <p>
                  {{ experience.details }}
                </p>
              </div>
              <div class="flex-shrink-0">
                <span class="text-primary">{{ experience.start_date }} - {{ experience.end_date }}</span>
              </div>
            </div>
          </div>
        </div>
      </section>
      <hr class="m-0" />
      <!-- Education-->
      <section class="resume-section" id="education">
        <div class="resume-section-content">
          <h2 class="mb-5">Education</h2>
          <div v-for="education in educations" :key="education.id">
            <div class="d-flex flex-column flex-md-row justify-content-between mb-5">
              <div class="flex-grow-1">
                <h3 class="mb-0">{{ education.university_name }}</h3>
                <div class="subheading mb-3">{{ education.degree }}</div>
                <div>{{ education.details }}</div>
              </div>
              <div class="flex-shrink-0">
                <span class="text-primary">{{ education.start_date }} - {{ education.end_date }}</span>
              </div>
            </div>
          </div>
        </div>
      </section>
      <hr class="m-0" />
      <!-- Skills-->
      <section class="resume-section" id="skills">
        <div class="resume-section-content">
          <h2 class="mb-5">Skills</h2>
          <ul class="fa-ul mb-0">
            <div v-for="skill in skills" :key="skill.id">
              <li>
                <span class="fa-li"><i class="fas fa-check"></i></span>
                {{ skill.name }}
              </li>
            </div>
          </ul>
        </div>
      </section>
      <hr class="m-0" />
      <!-- Capstones-->
      <section class="resume-section" id="capstones">
        <div class="resume-section-content">
          <h2 class="mb-5">Capstones</h2>
          <div v-for="capstone in capstones" :key="capstone.id">
            <div class="d-flex flex-column flex-md-row justify-content-between mb-5">
              <div class="flex-grow-1">
                <h3 class="mb-0">{{ capstone.name }}</h3>
                <div class="subheading mb-3">{{ capstone.url }}</div>
                <div>{{ capstone.description }}</div>
                <img :src="capstone.screenshot" />
              </div>
              <div class="flex-shrink-0"><span class="text-primary">August 2006 - May 2010</span></div>
            </div>
          </div>
        </div>
      </section>
      <hr class="m-0" />
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
      axios.get("https://evening-hollows-33474.herokuapp.com/resumes/" + this.$route.params.id).then((response) => {
        this.student = response.data;
        this.experiences = this.student.experiences;
        this.educations = this.student.education;
        this.skills = this.student.skills;
        this.capstones = this.student.capstones;
        console.log(response.data);
      });
    },
  },
};
</script>
