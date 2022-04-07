<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
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
      <v-card class="mx-auto my-12 px-4 py-4" max-width="500" v-if="!endFlag">
        <p>問題{{ counter + 1 }}</p>
        <p>{{ message }}</p>
        <p>{{ quizData[quizNow].quizText }}</p>
        <v-btn :disabled="nextBtn" v-for="(answer, index) in quizData[quizNow].answerList" :key="index" class="caption" small color="primary" @click="jadge(index)">{{ answer }}</v-btn>
        <!-- <p>今の問題番号：{{ quizNow }}<br>今の問題の正答：{{ answerListNow[ansNow] }}<br>今の問題の正答番号：{{ ansNow }}</p> -->
        <p><v-btn v-if="nextBtn" @click="nextQuiz()">次へ</v-btn></p>
      </v-card>
      <v-card class="mx-auto my-12 px-4 py-4" max-width="500" v-if="endFlag">
        <p>終了</p>
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      // 今の画面に出ている問題の番号
      quizNow: 0,
      // 正解のボタンの番号
      ansNow: 0,
      answerListNow: [],
      message: '',
      quizHistory: [],
      counter: 0,
      endFlag: false,
      quizData: [
        {
          quizText: '「音威子府」なんて読む？',
          answerList: [ 'おといねっぷ', 'おんいしふ', 'おといこふ', 'おんいこふ' ],
        },
        {
          quizText: '「長万部」なんて読む？',
          answerList: [ 'おしゃまんべ', 'ちょうまんぶ', 'ながまんべ', 'おさまんぶ' ],
        },
        {
          quizText: '「神居古潭」なんて読む？',
          answerList: [ 'かむいこたん', 'かみいこたん', 'しんきょこたん', 'しんいこたん' ],
        },
        {
          quizText: '「占冠」なんて読む？',
          answerList: [ 'しむかっぷ', 'せんかん', 'しめかん', 'せんかんむり' ],
        },
        {
          quizText: '「忍路」なんて読む？',
          answerList: [ 'おしょろ', 'にんろ', 'しのびみち', 'にんみち' ],
        },
        {
          quizText: '「銭函」なんて読む？',
          answerList: [ 'ぜにばこ', 'ぜにだて', 'せんかん', 'ぜにかん' ],
        },
      ],
      answerList: [],
    }
  },
  computed: {
    nextBtn() {
      // メッセージが空だったらtrue、そうじゃなかったらfalse
      return this.message == '' ? false : true
    }
  },
  methods: {
    quizNumber() {
      // 現在のクイズ番号をquizNowに代入
      this.quizNow =  Math.floor(Math.random() * this.quizData.length)
      // quizHistoryにquizNowの値があるかどうかをrに代入
      let r = this.quizHistory.includes(this.quizNow)
      while(r) { // rを満たしている間繰り返す
        this.quizNow =  Math.floor(Math.random() * this.quizData.length)
        r = this.quizHistory.includes(this.quizNow)
      }
      this.quizHistory.push(this.quizNow)
    },
    answerNumber() {
      // ans変数にanswerList[0]を入れておく(正解の文字をansに代入)
      const ans = this.quizData[this.quizNow].answerList[0]
      // ネットから持ってきたシャッフルするやーつ
      this.answerListNow = this.quizData[this.quizNow].answerList.sort(() => Math.random() - 0.5)
      // シャッフル後の配列内のans変数と同じ内容のものを探してその「位置」を調べる
      this.ansNow = this.answerListNow.findIndex(item => {
        return item === ans
      })
    },
    jadge(ansNumber) {
      if(ansNumber == this.ansNow) {
        this.message = '正解！'
      } else {
        this.message = '不正解！'
      }
    },
    // 次へボタンを押された時に実行するメソッド
    nextQuiz() {
      if(this.counter < 4) {
        this.counter++
        this.message = ''
        this.quizNumber()     // ランダムの数字から問題番号を決める
        this.answerNumber()   // 選択肢をシャッフルする
      } else {
        this.endFlag = true
      }
    }
  },
  // ページが読み込まれた時に1回だけ実行するcreated
  created() {
    this.quizNumber()     // ランダムの数字から問題番号を決める
    this.answerNumber()   // 選択肢をシャッフルする
  }
}
</script>
