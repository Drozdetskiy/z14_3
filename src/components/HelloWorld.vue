<template>
  <div>
    <input type="number" v-model="offset">
    <input type="number" v-model="limit">
    <button @click="getAllRecipes">Send request</button>
    <hr/>
    <p v-for="item in data">
      <strong>{{ item.title }}</strong>
    </p>
    <p>{{ position[1] }}</p>
    <p>{{ position[2] }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
      return {
          offset: 1,
          limit: 1,
          data: [],
          position: {
              1: "object1",
              2: "object2"
          }
      }
  },
  methods: {
      getAllRecipes () {
          setInterval(() => {
            axios.get('http://127.0.0.1:8000/api/recipes', {
            params: {
                offset: this.offset,
                limit: this.limit
            }
          })
          .then((response) => {
            this.data = response.data.results
          })
        }, 1000)

      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
