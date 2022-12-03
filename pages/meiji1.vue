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
  name: 'Meiji1Page',
  data() {
    return {
      show: false,
      questions: [
        '①1868年1月、旧幕府軍は新政府軍を相手に［　　］戦争を起こしましたが、翌年、降伏しました。',
        '②明治政府は、政治の方針として［　　］を出し、天皇を中心とする国家を目指すことを発表しました。',
        '③明治政府は、天皇を中心とした中央の政府が全国を直接納める中央集権国家を作るために［　　］を行い、土地と人民を天皇に返させました。',
        '④明治政府は［　　］を行い、これまでの藩を廃止し、新たに県や府を置き、政府が任命した県令（後の県知事）と府知事を派遣して治めさせました。',
        '⑤明治政府は［　　］を出し、満20歳になった男子に軍隊に入ることを義務づけました。',
        '⑥国の収入を安定させるために、明治政府は［　　］を行い、年貢ではなく土地に対する税である地租を現金で納めさせました。',
        '⑦明治時代、都市を中心に、生活の仕方やものの考え方が西洋風に変わっていったことを［　　］といいます。',
        '⑧慶應義塾（現在の慶應義塾大学）を創立した［　　］は『学問のすゝめ』を著しました。',
        '⑨明治政府は［　　］を公布して、全国に小学校をつくり、6歳以上の子供に教育を受けさせることを定めました。',
        '⑩1877年、西郷隆盛（さいごうたかもり）は九州で不平士族らとともに［　　］戦争を起こし、政府に武力で抵抗しましたが政府軍に敗れました。',
        '⑪国民が政治に参加するために、国民が選んだ議員による国会を開くことを求めて［　　］は、民撰議院設立（みんせんぎいんせつりつ）の建白書（けんぱくしょ）を政府に提出しました。',
        '⑫民撰議院設立の建白書をきっかけに、国会を開くことなどを求める［　　］運動が広まりました。',
        '⑬国会が開かれることが決まると、板垣退助（いたがきたいすけ）は、国民が進める政治を目指す［　　］党をつくりました。',
        '⑭国会が開かれることが決まると、大隈重信（おおくましげのぶ）は、議会と天皇が中心の政治を目指す［　　］党をつくりました。',
        '⑮秩父地方（ちちぶちほう）（埼玉県）で農民たちが、自由党員の指導のもと武器を持って立ち上がり、政府が警官隊や軍隊を出してしずめた事件を［　　］事件と言います。',
      ],
      question: undefined,
      answers: [
        '戊辰戦争（ぼしんせんそう）',
        '五箇条の御誓文（ごかじょうのごせいもん）',
        '版籍奉還（はんせきほうかん）',
        '廃藩置県（はいはんちけん）',
        '徴兵令（ちょうへいれい）',
        '地租改正（ちそかいせい）',
        '文明開化（ぶんめいかいか）',
        '福沢諭吉（ふくざわゆきち）',
        '学制（がくせい）',
        '西南戦争',
        '板垣退助（いたがきたいすけ）',
        '自由民権運動（じゆうみんけんうんどう）',
        '自由党',
        '立憲改進党（りっけんかいしんとう）',
        '秩父事件（ちちぶじけん）',
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
