<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <p>問題</p>
      <p>{{ quizData[questionNum].quizText }}</p>
      <p>
        <span v-for="answer in quizData[1].answerList" :key="answer">{{
          answer
        }}</span>
      </p>
      <v-btn color="primary">A</v-btn>
      <v-btn color="primary">B</v-btn>
      <v-btn color="primary">C</v-btn>
      <v-btn color="primary">D</v-btn>
      <div>
        <v-btn>次へ</v-btn>
      </div>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      quizData: [
        {
          quizText: '問題文1',
          answerList: [ '答えA', '答えB', '答えC', '答えD', ],
          answer: 0
        },
        {
          quizText: '問題文2',
          answerList: [ '答えA', '答えB', '答えC', '答えD', ],
        },
        {
          quizText: '問題文3',
          answerList: [ '答えA', '答えB', '答えC', '答えD', ],
        },
        {
          quizText: '問題文4',
          answerList: [ '答えA', '答えB', '答えC', '答えD', ],
        },
        {
          quizText: '問題文5',
          answerList: [ '答えA', '答えB', '答えC', '答えD', ],
        },
      ]
    }
  },
  computed: {
    questionNum: function() {
      return Math.floor(Math.random() * this.quizData.length)
    },

  }
}
</script>
