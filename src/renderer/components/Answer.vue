<template>
  <div id="wrapper">
      <v-btn fab small class="delete" @click="deleteItem">
        <v-icon>clear</v-icon>
      </v-btn>
      <v-card :color="color.main + ' ' + color.accent + '-' + color.index" class="white--text" @click="say">
        <v-card-title primary-title>
          <v-layout justify-center align-center>
            <div class="subheading"> {{ text }} </div>
          </v-layout>
        </v-card-title>
        <v-card-actions>
          <br>
        </v-card-actions>
      </v-card>
      <center v-show="shortcut">
        <v-btn class="shortcut" fab dark color="purple">
          [ {{ shortcut }} ]
        </v-btn>
      </center>
  </div>
</template>

<script>
  export default {
    name: 'Answer',
    props: [ 'text', 'color', 'shortcut', 'index' ],
    data: () => ({
    }),
    methods: {
      open (link) {
        require('electron').shell.openExternal(link)
      },
      say () {
        this.$emit('say', this.text)
      },
      deleteItem () {
        this.$emit('deleteItem', this.index)
      }
    }
  }
</script>

<style scoped>
  .shortcut{
    margin-top: -8vh;
  }

  #wrapper{
    margin: 2vh;
  }

  .delete{
    z-index: 4;
    opacity: 0.9;
    position : relative;
    margin-left: calc(100% - 20px);
    margin-bottom: -20px;
  }
</style>
