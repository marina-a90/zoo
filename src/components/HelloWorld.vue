<template>
  <div>

    <h1>ZOO</h1>

    <table style="width:100%">
      <tr>
        <th>Species</th>
        <th>Name</th> 
        <th>Birthday</th>
        <th>Remove from list</th>
      </tr>
      <tr v-for="(animal, index) in animals" :key="animal">
        <td>{{ animal.species }}</td>
        <td>{{ animal.name }}</td>
        <td v-if="animal.birthday">{{ animal.birthday }}</td>
        <td v-else>Nepoznat</td>
        <td><button @click="removeFromList(index)">Remove</button></td>
      </tr>
    </table>

  </div>
</template>

<script>
export default {
  data() {
    return {
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