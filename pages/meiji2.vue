<template>
  <div class="container">
    <div v-if="question">
      <p class="subtitle">{{question}}</p>
      <van-button 
        type="primary" 
        round 
        @click="showPopup">
        Next
      </van-button>
      <van-popup 
        v-model="show" 
        closeable
        position="bottom"
        :style="{ height: '30%' }"
        @close="closePopup">
        <div><p class="answer">{{answer}}</p></div>
      </van-popup>
    </div>
    <div v-if="!questions.length">
      <p class="subtitle">お疲れ様でした！</p>
      <van-button 
        type="warning" 
        round 
        @click="back">
        戻る
      </van-button>
      <van-button 
        type="primary" 
        round 
        @click="reload">
        もう一度
      </van-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Meiji2Page',
  data() {
    return {
      show: false,
      questions: [
        '①伊藤博文（いとうひろぶみ）はヨーロッパへ渡り、皇帝に権力が集中する［　　］の憲法を中心に学びました。',
        '②伊藤博文（いとうひろぶみ）は1885年に内閣制度（ないかくせいど）をつくり、自らが初代［　　］となりました。',
        '③1889年2月11日、当時アジアでただ1つの近代的な憲法であった［　　］が発布（はっぷ）されました。',
        '④1890年の第1回衆議院（しゅうぎいん）議員総選挙の有権者（ゆうけんしゃ）は、地租や所得税などの直接国に納める税金を［　　］円以上納める25歳以上の男子に限られ、国民の約1%だけでした。',
        '⑤1894年、朝鮮で東学（とうがく）（東学党）を中心とした甲午農民戦争（こうごのうみんせんそう）が起こると、日本と中国（清（しん））はそれぞれ軍隊を送り、［　　］戦争が始まりました。',
        '⑥日清戦争後に［　　］条約が結ばれ、日本は中国（清（しん））から新たな領土と多額の賠償金を得ました。',
        '⑦下関条約を結んだあと、ロシアはドイツ、フランスとともに、日本に対し遼東半島（りゃおとんはんとう）を清（しん）に返すように要求しました。これを［　　］といいます。',
        '⑧1904年、韓国と満州（まんしゅう）をめぐって、日本とロシアとの間に［　　］戦争が起こりました。',
        '⑨日露戦争の後、アメリカのルーズベルト大統領の仲立ちによって日本とロシアとの間で［　　］条約が結ばれました。',
        '⑩日清戦争で得た賠償金を使って官営（かんえい）の［　　］（福岡県）がつくられ、1901年から鉄鋼の生産が始まりました。',
        '⑪1910年、日本は［　　］を行い、韓国を植民地（しょくみんんち）としました。',
        '⑫1894年、外務大臣（がいむだいじん）［　　］は、外国が日本で持つ領事裁判権（りょうじさいばんけん）（治外法権（ちがいほうけん））の撤廃（てっぱい）に成功しました（条約の一部改正）。',
        '⑬1911年、外務大臣（がいむだいじん）［　　］が関税自主権（かんぜいじしゅけん）を回復し、条約の改正が達成されました。',
        '⑭［　　］は『坊っちゃん』『吾輩は猫である』などの作品を残しました。',
        '⑮［　　］は、蛇毒（へびどく）や黄熱病（おうねつびょう）の研究を行って、世界で認められました。',
      ],
      question: undefined,
      answers: [
        'ドイツ',
        '内閣総理大臣',
        '大日本帝国憲法（だいにっぽんていこくけんぽう）',
        '15円',
        '日清戦争（にっしんせんそう）',
        '下関条約（しものせきじょうやく）',
        '三国干渉（さんごくかんしょう）',
        '日露戦争（にちろせんそう）',
        'ポーツマス条約',
        '八幡製作所（やはたせいさくしょ）',
        '韓国併合（かんこくへいごう）',
        '陸奥宗光（むつむねみつ）',
        '小村寿太郎（こむらじゅたろう）',
        '夏目漱石（なつめそうせき）',
        '野口英世（のぐちひでよ）',
      ],
      answer: undefined,
      randomIndex: undefined,
    }
  },
  mounted() {
    this.doQuestion()
  },
  methods: {
    showPopup() {
      this.show = true;
    },
    closePopup() {
      this.reset()
      this.doQuestion()
    },
    reset() {
      this.questions.splice(this.randomIndex, 1)
      this.question = undefined
      this.answers.splice(this.randomIndex, 1)
      this.answer = undefined
      this.randomIndex = undefined
    },
    doQuestion() {
      setTimeout(() => {
        this.randomIndex = 0
        this.question = this.questions[this.randomIndex]
        this.answer = this.answers[this.randomIndex]
      }, 200)
    },
    back() {
      this.$router.push('/')
    },
    reload() {
      location.reload()
    }
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: Quicksand, 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 28px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.answer {
  font-weight: 300;
  font-size: 24px;
  color: #526488;
  word-spacing: 5px;
  padding-top: 40px;
}

.links {
  padding-top: 15px;
}
</style>
