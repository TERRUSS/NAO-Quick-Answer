<template>
  <v-app
    id="inspire"
    dark
  >
    <v-navigation-drawer
      v-model="drawer"
      fixed
      clipped
      app
    >
      <v-list dense>
        <v-subheader class="mt-3 grey--text text--darken-1">MENU</v-subheader>
        <v-list-tile v-for="item in items" :key="item.text" @click="">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>
              {{ item.text }}
            </v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-subheader class="mt-3 grey--text text--darken-1">MORE</v-subheader>
        <v-list-tile @click="">
          <v-list-tile-action>
            <v-icon color="grey darken-1">settings</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="grey--text text--darken-1">Settings</v-list-tile-title>
        </v-list-tile>
        <v-list-tile class="mt-3" @click="">
          <v-list-tile-action>
            <v-icon color="grey darken-1">help</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="grey--text text--darken-1">Infos</v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      color="deep-purple lighten-1"
      dense
      fixed
      clipped-left
      app
    >
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="mr-5 align-center">
        <span class="title text-uppercase">NAO</span>
        <span class="title text-uppercase font-weight-light">Quick</span>
        <span class="title text-uppercase">Answer</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-layout row align-center style="max-width: 650px">
        <v-text-field
          :append-icon-cb="() => {}"
          placeholder="Search..."
          single-line
          append-icon="search"
          color="white"
          hide-details
        ></v-text-field>
      </v-layout>
    </v-toolbar>

    <v-content>
      <v-container fill-height>
        <v-layout justify-center align-center wrap>
          <!-- <v-flex shrink> -->
            <Answer v-for="(answer, index) in answers"
            :key="index"
            :index="index"
            :text="answer.text"
            :color="answer.color"
            :shortcut="answer.shortcut"
            @say="say"
            @deleteItem="deleteItem"/>
          <!-- </v-flex> -->
        </v-layout>
      </v-container>
    </v-content>


    <AddButton @newAnswer="newAnswer"/>

  </v-app>

</template>

<script>
  import Answer from './components/Answer.vue'
  import AddButton from './components/AddButton.vue'

  export default {
    components: { Answer, AddButton },
    data: () => ({
      drawer: null,
      items: [
        { icon: 'star', text: 'Qick Answers' },
        { icon: 'audiotrack', text: 'Audio Files [COMMING SOON]' }
      ],
      answers: [
        { color: {main: 'red', accent: 'lighten', index: '2'}, text: 'Qick Answer', shortcut: 'Q' },
        { color: {main: 'green', accent: 'darken', index: '1'}, text: 'Macron démission', shortcut: 'M' }
      ]
    }),
    props: {
      source: String
    },
    methods: {
      say (text) {
        console.log(text)
      },
      deleteItem (index) {
        // delete an answer
        this.$data.answers.splice(index, 1)
      },
      newAnswer (answer) {
        console.log(this.answers)
        this.$data.answers.push(answer)
      }
    }
    // mounted: {
    //     // change title, icon
    //
    //   // XXX : connect with the NAO, etc
    //   /*
    //   var session = new QiSession("192.168.1.6");
    //
    //   session.socket().on('connect', function () {
    //     console.log('QiSession connected!');
    //     // now you can start using your QiSession
    //
    //     session.service("ALTextToSpeech").done(function (tts) {
    //
    //      tts.say("Evidemment que je kiff fornaïte fada");
    //
    //     }).fail(function (error) {
    //       console.log("An error occurred:", error);
    //     });
    //
    //   }).on('disconnect', function () {
    //     console.log('QiSession disconnected!');
    //   });
    //   */
    // }
  }
</script>

<style>
  @import "~vuetify/dist/vuetify.min.css";

  ::-webkit-scrollbar { display: none; }

  .v-toolbar {
    background: linear-gradient(to right, #d82bca 0%,#23d5db 100%,#7db9e8 100%);
  }

  #fab{
    bottom: 15px;
  }
</style>
