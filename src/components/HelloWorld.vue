<template>
  <div>

    <h1>ZOO</h1>

    <form @submit.prevent="addAnimal">
      <input type="text" v-model="animal.species" placeholder="species"/>
      <input type="text" v-model="animal.name" placeholder="name"/>
      <input type="text" v-model="animal.birthday" placeholder="birth date"/>
      <button type="submit">Add animal</button>
    </form>

    <table style="width:100%">
      <tr>
        <th>Species</th>
        <th>Name</th> 
        <th>Birthday</th>
        <th>Remove from list</th>
        <th>Move to top of the list</th>
      </tr>
      <tr v-for="(animal, index) in animals" :key="animal">
        <td>{{ animal.species }}</td>
        <td>{{ animal.name }}</td>
        <td v-if="animal.birthday">{{ animal.birthday }}</td>
        <td v-else>Nepoznat</td>
        <td><button @click="removeFromList(index)">Remove</button></td>
        <td><button @click="moveToTop(index)">Move to top</button></td>
      </tr>
    </table>

  </div>
</template>

<script>
export default {
  data() {
    return {
      animal: { species: "", name: "", birthday: "" },
      animals: [
        { species: "giraffe", name: "pera", birthday: "01.01.2000." },
        { species: "elephant", name: "sima", birthday: "01.01.2000." },
        { species: "tiger", name: "djoka", birthday: "01.01.2000." },
        { species: "gorilla", name: "jova", birthday: "" },
        { species: "parrot", name: "joca", birthday: "01.01.2000." }
      ]
    };
  },

  methods: {
    removeFromList(index) {
      let animal = this.animals[index];
      this.animals.splice(index, 1);
      alert(`${animal.species} removed from the list.`);
    },
    moveToTop(index) {
      let animal = this.animals[index];
      this.animals.splice(index, 1);
      this.animals.unshift(animal);
      alert(`${animal.species} moved to top of the list.`);
    },
    addAnimal() {
      let animal = {
        species: this.animal.species,
        name: this.animal.name,
        birthday: this.animal.birthday
      };
      this.animals.push(animal);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
}
</style>