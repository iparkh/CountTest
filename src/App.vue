<template>
<div class="training">
<h1>Математичний ...тренінг</h1> 
<hr>
<div class="progress">
  <div class="progress-bar" :style="progressStyles" ></div>
</div>
<div class="box">
  <transition name="flip" mode="out-in">
<app-start-screen v-if="state=='start'"
        @onStart="onStart"
>
</app-start-screen>
<app-message v-else-if="state=='message'"
             :type="message.type" 
             :text="message.text"
             @onNext="onNext"
>
</app-message>
<app-question v-else-if="state=='question'"
              :level="level+1"
              :settings="levels[level]"
              @success="onQuesSuccess"
              @error="onQuesError"
>
</app-question>
<app-result-screen v-else-if="state=='result'"
                   :stats="stats" 
                   :results="results"    
                   @repeate="onStart"
                   @nextLevel="onNextLevel"
>

</app-result-screen>
<div v-else>Незнайомий стан</div>
</transition>
</div>
</div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      state:'start',
      stats:{
        success:0,
        error:0        
      },
      results:[],
      message:{
        text:'qwer',
        type:'zxc'
      },
      quesMax:3,
      level: 0,
      levels:[
        {
          from :1,
          to:10,
          range:2,
          variants:2,
          ques:2
      },{
          from :1,
          to:15,
          range:4,
          variants:3,
          ques:20

      },{
          from :1,
          to:20,
          range:5,
          variants:4,
          ques:30

      },{
          from :10,
          to:30,
          range:6,
          variants:5,
          ques:30
      }
      ]

    }
  },
  computed:{
    questDone(){
      return this.stats.success+this.stats.error;
    },
    progressStyles(){
      return {
      //  width:(this.questDone/this.quesMax*100)+'%'
        width:(this.questDone/this.levels[this.level].ques*100)+'%'
      };
    }
  },
  methods:{
    addResult(x,y,z,secc){
      this.results.push({x:x,y:y,z:z,secc:secc});
    },
    onQuesSuccess(x,y,z){
      this.state='message';
      this.message.text='Добре';
      this.message.type='success';
      this.stats.success++;
      this.addResult(x,y,z,true);
    },
    onQuesError(msg,x,y,z){
      this.state='message';
      this.message.text=msg;
      this.message.type='warning';
      this.stats.error++;
      this.addResult(x,y,z,false);
    },
    onStart(){
      this.state='question';
      this.stats.success=0;
      this.stats.error=0;
    },
    onNextLevel(){
      this.level++;
      this.onStart();
    },
    onNext(){
     // if (this.questDone<this.quesMax) {
      if (this.questDone<this.levels[this.level].ques) {
      this.state='question';
      } else {
      this.state='result';  
      }
    }
  }
}
</script>

<style scoped>
.box{
  margin: 20px 0;
}
.training{
  max-width: 700px;
  margin: 20px auto;
}
.progress-bar{
  transition: width 0.5s;
}
.flip-enter{

}
.flip-enter-active{
  animation: flipInX 0.3s linear;
}
.flip-leave{
  
}
.flip-leave-active{
  animation: flipOutX 0.3s linear;
 
}
@keyframes flipInX{
  from {transform: rotateX(90deg);}
  to {transform: rotateX(0deg);}
}
@keyframes flipOutX{
  from {transform: rotateX(0deg);}
  to {transform: rotateX(90deg);}
}
</style>
