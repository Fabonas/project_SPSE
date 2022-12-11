<template>
  <main>
    <h1>Zoznam ľudí</h1>
    <section class="list">
      <section
        v-for="person of persons"
        v-bind:key="person"
        v-bind:class="{
          'card-container': true,
          card: true,
          adult: currentYear - person.birthday >= 18,
        }"
      >
        <!--v tomto prípade clase priradíme objekt, ktorého vlastnosti 
		  predstavujú jednotlivé triedy a ich hodnoti predstavujú bool 
		  vyjadrujúci, kedy sa má daná trieda pridať danému elemntu-->
        <!--alebo takto tu to poriešime ternárnym operátorom...
		<section v-for="person of persons" v-bind:key="person" 
		v-bind:class="person.age>=18 ? 'adult card-container card' : 'card-container card'">
		-->
        <article class="info">
          <div class="name">{{ person.fname }} {{ person.lname }}</div>
          <div class="age">
            <div class="birthday date">
              <span class="year-title"> Birthday year : </span>
              {{ person.birthday }}
            </div>
            <div class="birthday currentAge">
              <span class="year-title">Current age : </span>
              {{ currentYear - person.birthday }}
            </div>
          </div>
        </article>
        <footer class="footer-card">
          <span class="btn edit">Edit</span>
          <span class="btn remove">Remove</span>
        </footer>
      </section>
    </section>
  </main>
</template>

<script setup>
let currentDate = new Date();
let currentYear = currentDate.getFullYear();

let persons = [
  {
    fname: "Magdalena",
    lname: "Mikulova",
    birthday: 22,
  },
  {
    fname: "Mirka",
    lname: "Makovicova",
    birthday: 30,
  },
  {
    fname: "Hugo",
    lname: "Hugovic",
    birthday: 15,
  },
  {
    fname: "Miki",
    lname: "Hric",
    birthday: 19,
  },
  {
    fname: "Andrea",
    lname: "Veresova",
    birthday: 40,
  },
  {
    fname: "Nora",
    lname: "Mojsejova",
    birthday: 13,
  },
];

const changeBirthday = () => {
  persons.forEach((person) => {
    person.birthday = currentYear - person.birthday;
  });
};

changeBirthday();
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Oswald:wght@200;300;500;600;700&display=swap");
body {
  font-size: 10px;
  font-family: "Oswald", sans-serif;
  font-weight: 800;
  padding: 1rem;
}
main {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

main > h1 {
  text-align: center;
}

.list {
  display: flex;
  gap: 20px;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: stretch;
  font-size: 1.2rem;
}
.card-container {
  flex-grow: 1;
}
.card {
  background: rgba(255, 255, 255, 1);
  border: 1px solid #bbb;
  color: rgb(49, 49, 49);
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.2);
  border-top-width: 5px;
  border-top-color: dodgerblue;
  border-radius: 8px;
}
.card.adult {
  border-top-color: orange;
}
.card:hover {
}
.info {
  padding: 1rem;
  text-align: center;
  font-size: 1.3rem;
}
.name {
}
.age {
  font-weight: 300;
  font-size: 1rem;
  font-weight: 300;
  display: flex;
  flex-direction: column;
}
.year-title {
  color: #b9b9b9;
  font-weight: 400;
}
.footer-card {
  display: flex;
}
.btn {
  padding: 0.75rem 2rem;
  color: beige;
  width: 50px;
  flex-grow: 1;
  text-align: center;
  transition: 0.5s;
  font-size: 1rem;
  font-weight: 300;
}
.btn.edit {
  background: rgb(36, 201, 36);
  border-bottom-left-radius: 8px;
}
.btn.remove {
  background: rgb(180, 27, 27);
  border-bottom-right-radius: 8px;
}
.btn:hover {
  opacity: 0.3;
  cursor: pointer;
}
</style>
