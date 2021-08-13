<template>
  <div class="students-index">
    <div v-for="student in students" :key="student.id">
      <section class="resume-section" id="experience">
        <router-link v-bind:to="`/students/${student.id}`">
          <div class="resume-section-content">
            <div class="d-flex flex-column flex-md-row justify-content-between mb-5">
              <div class="flex-grow-1">
                <img :src="student.photo_url" alt="no image found" />
                <h3 class="mb-0">{{ student.first_name }} {{ student.last_name }}</h3>
                <p>
                  {{ student.bio }}
                </p>
              </div>
            </div>
          </div>
        </router-link>
      </section>
    </div>
    <hr class="m-0" />
    <nav class="navbar navbar-expand-lg navbar-dark bg-primary fixed-top" id="sideNav">
      <span class="d-none d-lg-block">
        <img
          class="img-fluid img-profile rounded-circle mx-auto mb-2"
          src="https://t3.ftcdn.net/jpg/03/77/85/04/360_F_377850455_Gk0rRBzegH6YX9SZK9YbgyYyLwrVb9zi.jpg"
          alt="..."
        />
      </span>
    </nav>
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
      axios.get("https://evening-hollows-33474.herokuapp.com/students").then((response) => {
        this.students = response.data;
        console.log("all students", this.students);
      });
    },
  },
};
</script>

<style>
.rounded-circle {
  width: 250px;
}
img {
  width: 400px;
}
</style>
