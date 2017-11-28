<template>
  <div class="container">
    <div class="row" v-for='row in arr'>
      <div class="col" v-for='col in row'>
        <span @click="tryBumb(col)" class="field" :class="bombs(col)">
          {{col}}
        </span>
      </div>


    </div>
    <!-- {{arr}} -->
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      arr:[],
      succ:0
    }
  },
  methods:{
    bombs(col){
      if(col.click){
        if(col.bomb){
          return 'bomb'
        }
        else {
          return 'safe'
        }
      }
      else {
        return ''
      }
    },
    tryBumb(col){
      let n = 5
      let m = 5
      for(let i=0;i<n;i++){
        for(let j=0;j<m;j++){
          if(this.arr[i][j].num === col.num){
            this.$set(this.arr[i][j],'click',true)
          }
        }
      }
    },
    getRandNum(max,min){
      let result = []
      let randNum = Math.floor( Math.random() * (max - min + 1) ) + min;
      while(result.length < 5){
        if(!result.includes(randNum)){
          result.push(randNum)
        }
        randNum = Math.floor( Math.random() * (max - min + 1) ) + min;
      }
      return result
    },
    setBomb(num){
      let bombs = this.getRandNum(25,1)
      let n = 5
      let m = 5
      bombs.forEach(item => {
        for(let i=0;i<n;i++){
          for(let j=0;j<m;j++){
            if(this.arr[i][j].num === item){
              this.$set(this.arr[i][j],'bomb',true)
            }
          }
        }
      })
    }
  },
  created(){
    let n = 5
    let m = 5
    let count = 1
    for(let i=0;i<n;i++){
      this.$set(this.arr,i,[])
      for(let j=0;j<m;j++){
        let obj = {
          "num":count,
          "click":false,
          "bomb":false
        }
        this.$set(this.arr[i],j,obj)
        // this.$set(this.arr[i][j],'num',count)
        // this.$set(this.arr[i][j],'click',false)
        // this.$set(this.arr[i][j],'bomb',false)
        count = count + 1
      }
    }
    this.setBomb(5)

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.col{
  display: inline-block;
}
.field{
  display: inline-block;
  width: 100px;
  height: 100px;
  border: 1px red solid;
}
.bomb{
  background-color: red;
}
.safe{
  background-color: green;
}
</style>
