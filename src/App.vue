<template>

  <div class="">

    <ul>
      <li v-for="state in states" :key="state">{{state.nome}}</li>
    </ul>

  </div>



</template>

<script>

export default {

  data() {
    return {
      states: []
    }
  },

  created() {

    fetch('https://servicodados.ibge.gov.br/api/v1/localidades/estados')
    .then(response => {
      response.json().then(data => {
        this.states = data;
      }).catch(err => {
        console.log(err)
      })
    })
  },

  methods: {

    // i can create methods it this way
    reverseMessage() {
      alert('fui clicado')
      this.message = 'esse botao foi clicado'
    },

  // or this way
    alterarTextoNoClick: function() {
      this.message = 'esse botao foi clicado'
    }
  },

  computed : {

    fulllName: {
      get: function() {
        return `${this.person.firstName} ${this.person.lastName}`
      },
      set: function(newValue) {
        let name = newValue.split(' ')

        this.person.firstName = name[0]
        this.person.lastName = name[1]
      }
    }
  }
}
</script>

<style>

li {
  color: black;
}

</style>
