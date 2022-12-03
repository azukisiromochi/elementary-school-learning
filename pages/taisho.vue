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
        '①1914年、「ヨーロッパの火薬庫」と呼ばれるバルカン半島で起きたサラエボ事件がきっかけとなり、多くの国々を巻き込む［　　］が始まりました。',
        '②第一次世界大戦に連合国側（れんごうこくがわ）として参戦した日本は、中国に対し［　　］の要求を出して、強引に大部分を認めさせました。',
        '③第一次世界大戦中の1917年、ロシアでは［　　］革命が起こり、世界で初めて社会主義政府が誕生しました。',
        '④シベリア出兵に際して（さいして）商人が米を買いしめたため米の値段が上がり、1918年には人々が米屋をおそうなどの［　　］が起こりました。',
        '⑤第一次世界大戦でドイツが降伏（こうふく）すると連合国側が勝利し、1919年、パリ講和会議（こうわかいぎ）が開かれ、［　　］条約が結ばれました。',
        '⑥パリ講和会議（こうわかいぎ）でアメリカのウィルソン大統領は［　　］の考えを提案し、ヨーロッパでは多くの国々が独立しました。',
        '⑦日本の植民地支配に苦しむ朝鮮では、1919年3月1日に独立運動が起こり、国内に広まりました（［　　］独立運動）。',
        '⑧日本の支配に苦しむ中国では、1919年5月4日に二十一か条の要求の取り消しを求める運動が起こり、国内に広まりました（［　　］運動）。',
        '⑨パリ講和会議（こうわかいぎ）でウィルソン大統領は世界の平和を守るための組織をつくることを提案し、1920年に［　　］が誕生しました。',
        '⑩1912年、犬養毅（いぬかいつよし）や尾崎行雄（おざきゆきお）らは藩閥政治（はんばつせいじ）を批判し、憲法の考えをもとに人々の考えを政治に取り入れようという［　　］運動を起こしました。',
        '⑪1918年、原敬（はらたかし）は、ほとんどの大臣が自分の所属する政党の党員から成る、初めての本格的な［　　］をつくりました。',
        '⑫［　　］は財産による制限がない普通選挙の実施を求めるなど、民本主義（みんぽんしゅぎ）を唱えました。',
        '⑬［　　］は青鞜社（せいとうしゃ）をつくって、女性の地位と権利の向上を目指す運動を広げました。',
        '⑭加藤高明内閣（かとうたかあきないかく）ができると、1925年、25歳以上の全ての男子が選挙権を持つ［　　］が成立しました。',
        '⑮普通選挙法が定められた一方で、社会主義者を取りしまる理由で、［　　］が成立しました。',
      ],
      question: undefined,
      answers: [
        '第一次世界大戦',
        '二十一か条の要求',
        'ロシア革命',
        '米騒動',
        'ベルサイユ条約',
        '民族自決（みんぞくじけつ）',
        '三・一独立運動（さんいちどくりつうんどう）',
        '五・四運動（ごしうんどう）',
        '国際連盟（こくさいれんめい）',
        '護憲運動（ごけんうんどう）',
        '政党内閣（せいとうないかく）',
        '吉野作造（よしのさくぞう）',
        '平塚らいてう（「平塚雷鳥」でもよい）',
        '普通選挙法（ふつうせんきょほう）',
        '治安維持法（ちあんいじほう）',
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
