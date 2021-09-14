<template>
  <div id="timerComponent">
    <div class='timer_text'>
      <p  v-show="!active" class="setted_time">{{study_time}}</p>
      <p  v-show="active" class="time_left">{{time_left}}</p>
    </div>
    <form class="timer_form">
      <div>アラーム: 
        <select 
          class ='select_hour'
          v-model="setted_hour"
        >
          <option 
            v-for="n in 21"
            v-bind:key="n"
          >
          {{n-1 | adjustDigit}}
          </option>
        </select>
        <select 
          class ='select_minute'
          v-model="setted_minute"
        >
          <option 
            v-for="n in 60"
            v-bind:key="n"
          >
          {{n-1 | adjustDigit}}
          </option>
        </select>
      </div>
    </form>
    <div 
      class="start_btn"
      v-show="!active"
      v-on:click="startTimer"
    >start</div>
    <div 
      class="cancel_btn"
      v-show="active"
      v-on:click="cancelTimer"
    >cancel</div>
    <div 
      class="pause_btn"
      v-show="active"
      v-on:click="active = !active"
    >pause</div>
  </div>
</template>

<script>
export default {
  name:'timerComponent',
  data(){
    return {
      setted_hour:'00',
      setted_minute:'00',
      study_time:'00:00:00',
      time_left:'',
      active:false,
    }
  },
  filters:{
    adjustDigit(number){
      if(number < 10){
        return `0${number}`;
      }
      return number;
    }
  },
  watch:{
    setted_hour(){
      this.study_time = `${this.setted_hour}:${this.setted_minute}:00`;
    },
    setted_minute(){
      this.study_time = `${this.setted_hour}:${this.setted_minute}:00`;
    }
  },
  methods:{
    startTimer(){
      this.active = true;
      const startTime = Date.now();
      this.countDown(startTime);
    },
    countDown(startTime){
      //経過時間
      const elapsed_time = Date.now() - startTime;
    
      //設定した時間 ミリ秒に直す
      const setted_time = `${this.setted_hour*3600 + this.setted_minute*60}000`;

      //残り時間を算出
      const left = new Date(setted_time - elapsed_time);
      const h = String(left.getHours()-9).padStart(2,'0');
      const m = String(left.getMinutes()).padStart(2,'0');
      const s = String(left.getSeconds()).padStart(2,'0');
      this.time_left = `${h}:${m}:${s}`

      //イベントループ
      let timeoutId = setTimeout(()=>{
        this.countDown(startTime);
      },1000)

      //時間切れでsetTimeoutを止める 1秒誤差あり
        if(Math.floor((setted_time - elapsed_time)/1000) < 1){
        clearTimeout(timeoutId);
        this.addRecord();
        this.active = false;
      }
    },
    cancelTimer(){
      clearTimeout(this.timeoutId);
      this.active = false;
    },
    addRecord(){
      console.log('ok')
    }
  }
}
</script>
