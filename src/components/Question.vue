<template>
  <div class="alert">
    <h3>Рівень {{level}}</h3>
    <h3>
      {{x}}+{{y}}={{answer}}
    </h3>
    <div class="buttons">
      <button class="btn btn-primary"
               v-for="number in answers" 
               @click="onAnswer(number)">
      {{number}}
      </button>
    </div>
  </div>
</template>

<script>
export default{
  props:['level','settings'],
  data(){
    return {
      answer:'',
      x:mtRand(this.settings.from,this.settings.to),
      y:mtRand(this.settings.from,this.settings.to)
    }
  },
  methods:{
    onAnswer(num){
      if (num===this.good){
      this.$emit('success',1,2,3);
      //this.$emit('success');
      } else {
      //this.$emit('error',`Вірно так : ${this.x} + ${this.y} = ${this.good}`,thus.x,this.y,this.good)
      this.$emit('error',`Вірно так : ${this.x} + ${this.y} = ${this.good}`,0,2,3)
      }
    }
  },
  computed:{
    good(){
      return this.x+this.y;  
    },
    answers(){
      //let good=this.good;
      let res=[this.good];
          //res.push(good) ; 
      while(res.length<this.settings.variants){
      let num= mtRand(this.good-this.settings.range,this.good+this.settings.range); 
      if (res.indexOf(num)===-1) {
          res.push(num) ;  
      }
      }
      return res.sort(function(){
        return Math.random()>0.5;
      });
    }
  }
}
function mtRand(min,max) {
  let diff=max-min;
  return Math.floor(Math.random()*(diff+1))+min;
}
</script>

<style scoped>
.alert{
  text-align: center;
  padding-top: 20px;
  background-color: #eee;
}
.buttons{
  display:flex;
  justify-content: space-around;
  
}
.btn{
  margin:20px 0;
}
</style>