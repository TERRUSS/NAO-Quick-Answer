<template>

  <div id="addButton">
    <v-btn
      color="purple accent-2"
      dark
      absolute
      bottom
      right
      fab
      @click="dialog = !dialog"
      id="fab"
    >
      <v-icon>add</v-icon>
    </v-btn>
    <v-dialog v-model="dialog" max-width="500px">
      <v-card>
        <v-card-text>
          <v-icon>message</v-icon>&nbsp;&nbsp;
          <v-text-field label="Nouveau messsage" v-model="newAnswer.text" @keyup.enter="newAnswerSubmit"></v-text-field>
          <v-icon>keyboard</v-icon>&nbsp;&nbsp;
          <v-text-field label="Shortcut" v-model="newAnswer.shortcut" @keyup.enter="newAnswerSubmit"></v-text-field>
          <!-- <v-text-field label="Couleur" v-model="newAnswer.color" @keyup.enter="newAnswerSubmit"></v-text-field> -->
          <v-icon>color_lens</v-icon>&nbsp;&nbsp;
          <v-layout>
            <v-flex>
              <v-autocomplete
              v-model="newAnswer.color.main"
              :items="['red', 'pink', 'purple', 'deep-purple', 'blue', 'cyan', 'teal', 'green', 'yellow', 'orange', 'brown']"
              label="Couleur"
              required
              ></v-autocomplete>
            </v-flex>
            <v-flex>
              <v-autocomplete
              v-model="newAnswer.color.accent"
              :items="['lighten', 'darken', 'accent']"
              label="Accent"
              ></v-autocomplete>
            </v-flex>
            <v-flex>
              <v-select
                v-model="newAnswer.color.index"
                :items="['1', '2', '3', '4']"
                label="Index"
              ></v-select>
            </v-flex> &nbsp;
          </v-layout>
        </v-card-text>
        <center>
          <v-btn large :color="newAnswer.color.main + ' ' + newAnswer.color.accent + '-' + newAnswer.color.index" @click="newAnswerSubmit">Submit</v-btn>
        </center>
      </v-card>
    </v-dialog>
  </div>

</template>


<script>
  export default {
    name: 'AddButton',
    data: () => ({
      dialog: false,
      newAnswer: {
        color: {main: 'cyan', accent: 'lighten', index: '2'},
        text: '',
        shortcut: ''
      }
    }),
    methods: {
      newAnswerSubmit () {
        // add button
        this.$emit('newAnswer', this.$data.newAnswer)

        // close & reset dialog
        this.$data.dialog = false
        this.$data.newAnswer = {color: {main: 'cyan', accent: 'lighten', index: '2'}, text: '', shortcut: ''}
      }
    }
  }
</script>
