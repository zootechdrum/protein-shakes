<template>
  <div class="index container">
    <div class="card" v-for="smoothie in smoothies" :key="smoothie.id">
      <div class="card-content">
        <i class="material-icons delete" @click="deleteSmoothie(smoothie.id)">delete</i>
        <h2 class="indigo-text">{{ smoothie.title }}</h2>
        <ul class="ingrerdients">
          <li v-for="(ing, index) in smoothie.ingrerdients" :key="index">
           <span class="chip"> {{ ing }}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

import db from '@/firebase/init'

export default {
  name: 'Index',
  data () {
    return {
      smoothies: [ ]
    }
  },
  methods:{
    deleteSmoothie(id) {
      this.smoothies = this.smoothies.filter(smoothie => {
        return smoothie.id !== id;
      })
    }
  },
  created() {
    db.collection("smoothies").get()
      .then(snapshot => {
        snapshot.forEach(doc => {
          console.log(doc)
        })
      }
    )
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

.index {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 30px;
  margin-top: 60px;

}

.index h2 {
  text-align: center;
  font-size: 1.8rem;
}

.index .ingrerdients{
  margin-top: 30px auto;
}

.index .ingrerdients li {
  display:inline-block;
}

.index .delete {
  position:absolute;
  top:4px;
  right: 4px;
  font-size: 1.4em;
  cursor: pointer;
}

</style>
