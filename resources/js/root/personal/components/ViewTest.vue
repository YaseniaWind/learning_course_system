<template>
  <div>
   <div v-if="!testr">
 <div v-for="test in testItems" :key="test.id" style="margin-bottom: 25px;">
    <b>{{test.quest}}</b>

    Варианты ответа: <br>
    <ul v-for=" t in test.anserws" :key="t.q">
    {{t.q}} <input type="radio" id="one"   @click="test.useransers = t.q "/>


    </ul>
  <span>Выбрано: {{ test.useransers }}</span>

    </div>
    <br>
     <button @click="ShowResult">Показать результаты </button>
   </div>



<div v-else>
<div v-for="r in currentResult" :key="r">
<li>Вопрос : {{r.questTest}}</li>
<li>Ваш ответ : {{r.anserwsUser}}</li>
<li>Правильный ответ : {{r.trueAnserw}}</li>
</div>
<li v-if="ball">Общий бал в этом тесте составил: {{ball}} % </li>
<center> <button  class="btn btn-outline-danger" @click="$emit('getResult', ball) ">Получить сертификат</button></center>
</div>
  </div>

</template>

<script>
export default {
  data(){
    return {
      testr: null,
      currentResult: [],
      testItems: JSON.parse(this.testItemsData),
      currentscore: null,
      score: null,
      scorearr: [],
      ball: null,

    }
  },
  props:{
    testItemsData: Array
  },
  methods:{
    ShowResult(){




      let trueresulttest
      let trueresulttestq
      this.testItems.map((item) =>{
        item.anserws.forEach(i =>{
          if(i.t === true){
            trueresulttest = i.t
            trueresulttestq = i.q
          }
        })
        // console.log(trueresulttest)

        let resultTest = {
          questTest : item.quest,
          anserwsUser: item.useransers,
          trueAnserw: trueresulttestq
        }
        this.currentResult.push(resultTest)
        // console.log(item.useransers)

      }
      )
      this.testr = true;


      this.currentResult.forEach(element => {
        if(element.anserwsUser === element.trueAnserw){
             this.scorearr.push(element.anserwsUser)
        }

      });

       this.currentscore = Object.keys(this.testItems).length;
        console.log(this.currentscore);

        this.score = Object.keys(this.scorearr).length;
         console.log(this.score);

         this.ball = (this.score / this.currentscore) *100;

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
