<template>
  <div>

    <h1>ZOO</h1>

    <form @submit.prevent="addAnimal">
      <input type="text" v-model="animal.species" placeholder="species"/>
      <input type="text" v-model="animal.name" placeholder="name"/>
      <input type="text" v-model="animal.birthday" placeholder="birth date"/>

    <select v-model="animal.sector">
      <option v-for="sector in sectors" :key="sector" :value="sector">{{ sector }}</option>
    </select>

      <button type="submit">Add animal</button>
    </form>

    <table style="width:100%">
      <tr>
        <th>Species</th>
        <th>Name</th> 
        <th>Birthday</th>
        <th>Sector</th>
        <th>Remove from list</th>
        <th>Move to top of the list</th>
      </tr>
      <tr v-for="(animal, index) in animals" :key="index">
        <td>{{ animal.species }}</td>
        <td>{{ animal.name }}</td>
        <td v-if="animal.birthday">{{ animal.birthday }}</td>
        <td v-else>Nepoznat</td>
        <td>{{ animal.sector }}</td>
        <td><button @click="removeFromList(index)">Remove</button></td>
        <td><button @click="moveToTop(index)">Move to top</button></td>
      </tr>
    </table>

    <table style="width:50%">
      <tr>
        <th>Sectors</th>
      </tr>
      <tr v-for="(sector, index) in sectors" :key="index">
        <td>{{ sector }}</td>
        <td><button @click="seeAllFromSector(index)">See all {{ sector }}s</button></td>
      </tr>
    </table>

  </div>
</template>

<script>
export default {
  data() {
    return {
      animal: { species: "", name: "", birthday: "", sector: "" },
      animals: [
        {
          species: "giraffe",
          name: "pera",
          birthday: "01.01.2000.",
          sector: "mamal"
        },
        {
          species: "elephant",
          name: "sima",
          birthday: "01.01.2000.",
          sector: "mamal"
        },
        {
          species: "tiger",
          name: "djoka",
          birthday: "01.01.2000.",
          sector: "mamal"
        },
        { species: "gorilla", name: "jova", birthday: "", sector: "mamal" },
        {
          species: "parrot",
          name: "joca",
          birthday: "01.01.2000.",
          sector: "mamal"
        }
      ],
      sectors: ["mamal", "bug"]
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
        birthday: this.animal.birthday,
        sector: this.animal.sector
      };
      this.animals.push(animal);
    },
    seeAllFromSector(index) {
      let sector = this.sectors[index];
      console.log(sector);
      let animalsInSector = this.animals.filter(
        animal => sector === animal.sector
      );
      let sectorList = [];
      let msg = "";
      this.animals.forEach(function(animal) {
        if (sector === animal.sector) {
          sectorList.push(animal.species);
        }
      });
      if (sectorList.length > 0) {
        msg = `Animals from ${sector}s are ${[...sectorList]}`;
      } else {
        msg = "There are not animals in this sector :(";
      }
      alert(msg);
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