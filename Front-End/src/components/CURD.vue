<template>
  <div class="container">
    <div class="input">
      <span>Name:</span>
      <input type="text" v-model="name" />
    </div>
    <div class="input">
      <span>Id:</span>
      <input type="text" v-model="id" />
    </div>
    <!-- buttons -->
    <div class="btn-container">
      <div class="button">
        <button class="btn" @click="addPerson()">Add</button>
      </div>
      <div class="button">
        <button class="btn" @click="getPerson()">Get</button>
      </div>
      <div class="button">
        <button class="btn" @click="deletePerson()">Delete</button>
      </div>
      <div class="button">
        <button class="btn" @click="getAll()">Get All</button>
      </div>
      <div class="button">
        <button class="btn" @click="update()">Update</button>
      </div>
    </div>
    <li class="person" v-for="person in people" :key="person.name">{{person.name}} - {{person.id}}</li>
  </div>
</template>

<script>
import axios from "axios";
// import qs from "qs";

const base_url = "http://localhost:8888/api/v1/person";

export default {
  name: "CURD",
  data() {
    return {
      name: "",
      id: "",
      people: []
    };
  },
  methods: {
    update() {
      axios
        .put(
          base_url + "/" + this.id,
          {
            name: this.name
          },
          {
            headers: {
              "Content-Type": "application/json"
            }
          }
        )
        .then(response => {
          this.getAll();
          this.id = '';
          this.name = '';
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
    },
    getPerson() {
      axios
        .get(base_url + "/" + this.id)
        .then(response => {
          this.people = [];
          this.people.push(response.data);
          this.id = '';
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
    },
    deletePerson() {
      axios
        .delete(base_url + "/" + this.id)
        .then(response => {
          this.getAll();
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
    },
    getAll() {
      axios
        .get(base_url)
        .then(response => {
          this.people = response.data;
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
    },
    addPerson() {
      axios
        .post(
          base_url,
          {
            name: this.name,
            id: this.id
          },
          {
            headers: {
              "Content-Type": "application/json"
            }
          }
        )
        .then(response => {
          this.getAll();
          this.id = '';
          this.name = '';
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
:root {
  /* dark shades of primary color*/
  --clr-primary-1: hsl(205, 86%, 17%);
  --clr-primary-2: hsl(205, 77%, 27%);
  --clr-primary-3: hsl(205, 72%, 37%);
  --clr-primary-4: hsl(205, 63%, 48%);
  /* primary/main color */
  --clr-primary-5: #49a6e9;
  /* lighter shades of primary color */
  --clr-primary-6: hsl(205, 89%, 70%);
  --clr-primary-7: hsl(205, 90%, 76%);
  --clr-primary-8: hsl(205, 86%, 81%);
  --clr-primary-9: hsl(205, 90%, 88%);
  --clr-primary-10: hsl(205, 100%, 96%);
  /* darkest grey - used for headings */
  --clr-grey-1: hsl(209, 61%, 16%);
  --clr-grey-2: hsl(211, 39%, 23%);
  --clr-grey-3: hsl(209, 34%, 30%);
  --clr-grey-4: hsl(209, 28%, 39%);
  /* grey used for paragraphs */
  --clr-grey-5: hsl(210, 22%, 49%);
  --clr-grey-6: hsl(209, 23%, 60%);
  --clr-grey-7: hsl(211, 27%, 70%);
  --clr-grey-8: hsl(210, 31%, 80%);
  --clr-grey-9: hsl(212, 33%, 89%);
  --clr-grey-10: hsl(210, 36%, 96%);
  --clr-white: #fff;
  --clr-red-dark: hsl(360, 67%, 44%);
  --clr-red-light: hsl(360, 71%, 66%);
  --clr-green-dark: hsl(125, 67%, 44%);
  --clr-green-light: hsl(125, 71%, 66%);
  --clr-secondary: hsla(182, 63%, 54%);
  --clr-black: #222;
  --ff-primary: "Roboto", sans-serif;
  --ff-secondary: "Open Sans", sans-serif;
  --transition: all 0.3s linear;
  --spacing: 0.25rem;
  --radius: 0.5rem;
  --light-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  --dark-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  --max-width: 1170px;
  --fixed-width: 620px;
}

.input {
  display: block;
  margin: 1rem 1rem;
}

.button {
  display: inline-block;
  padding: 1rem 1rem;
}

.btn {
  text-transform: uppercase;
  background: transparent;
  color: var(--clr-black);
  padding: 0.375rem 0.75rem;
  letter-spacing: var(--spacing);
  display: inline-block;
  transition: var(--transition);
  font-size: 0.875rem;
  border: 2px solid var(--clr-black);
  cursor: pointer;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
  border-radius: var(--radius);
}

.btn:hover {
  background: var(--clr-black);
  color: var(--clr-secondary);
}
</style>
