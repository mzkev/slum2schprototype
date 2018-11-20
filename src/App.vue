<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Slum2School Prototype</h1>
    </div>
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3> Add A Student</h3>
      </div>
      <div class="panel-body">
        <form id="form" class="form-control" v-on:submit.prevent="addStudent">
          <div class="form-group">
            <label for="fullName"> Full Name: </label>
            <input type="text" id="fullName" class="form-control" v-model="newStudent.fullName" />
          </div>
          <div class="form-group">
            <label for="age"> Age: </label>
            <input type="number" id="age" class="form-control" v-model="newStudent.age"/>
          </div>
          <div class="form-group">
            <label for="gender"> Gender: </label>
            <input type="text" id="gender" class="form-control" v-model="newStudent.gender"/>
          </div>
          <div class="form-group">
            <label for="parentGuardianName"> Parent's/ Guardian's Name: </label>
            <input type="text" id="parentGuardianName" class="form-control" v-model="newStudent.parentGuardianName"/>
          </div>
          <div class="form-group">
            <label for="state"> State: </label>
            <input type="text" id="state" class="form-control" v-model="newStudent.state"/>
          </div>
          <div class="form-group">
            <label for="schoolName"> School Name: </label>
            <input type="text" id="schoolName" class="form-control" v-model="newStudent.schoolName"/>
          </div>
          <input type="submit" class="btn btn-primary" value="Add Student"/>
        </form>
      </div>
    </div>
     <div class="panel panel-default view">
      <div class="panel-heading">
        <h3>
          Students Details
         </h3>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>
                Full Name
                </th>
                <th>
               Age
                </th>
                <th>
                Gender
                </th>
                <th>
                Parent's/ Guardian's Name
                </th>
                <th>
                State
                </th>
                <th>
               School's Name
                </th>
              </tr>
          </thead>
          <tbody>
            <tr v-for="student in studentDetails" :key="student.id">
              <td> {{ student.fullName}}</td>
              <td> {{ student.age}}</td>
              <td> {{ student.gender}}</td>
              <td> {{ student.parentGuardianName}}</td>
              <td> {{ student.state}}</td>
              <td> {{ student.schoolName}}</td>
              </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import Firebase from "firebase";
let config = {
  apiKey: "AIzaSyD7kfvj6aLR15fADRsqt3G1gcboUeVjn60",
  authDomain: "slum2school-e5b5a.firebaseapp.com",
  databaseURL: "https://slum2school-e5b5a.firebaseio.com",
  projectId: "slum2school-e5b5a",
  storageBucket: "slum2school-e5b5a.appspot.com",
  messagingSenderId: "290380161194"
};

let app = Firebase.initializeApp(config);
let db = app.database();

let studentDetailsRef = db.ref("studentDetails");

export default {
  name: "App",
  firebase: {
    studentDetails: studentDetailsRef
  },
  data() {
    return {
      newStudent: {
        fullName: "",
        age: "",
        gender: "",
        parentGuardianName: "",
        state: "",
        schoolName: ""
      }
    };
  },
  methods: {
    addStudent: function() {
      studentDetailsRef.push(this.newStudent);
      this.newStudent.fullName = "";
      this.newStudent.age = "";
      this.newStudent.gender = "";
      this.newStudent.parentGuardianName = "";
      this.newStudent.state = "";
      this.newStudent.schoolName = "";
    }
  }
};
</script>

<style>
.view {
  margin-top: 45%;
}
</style>
