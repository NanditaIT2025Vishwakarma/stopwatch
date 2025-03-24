# stopwatch<!DOCTYPE html>

<html lang="en" dir="ltr">
  <head>
    <meta charset="UTF-8">
    <title> Stopwatch Timer application  </title> 
    <link rel="stylesheet" href="style.css">
   </head>
<style>


@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins',sans-serif;
}
body{
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #000000;
}
.wrapper{
  user-select: none;
}
.wrapper .time{
  height: 100px;
  background: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 6px;
  box-shadow: 10px 10px 20px rgba(0,0,0,0.09);
  padding: 0 10px;
}
.wrapper .time span{
  width: 100px;
  text-align: center;
  font-size: 50px;
  font-weight: 500;
  color: #333;
}
.time span.colon{
  width: 10px;
}
.time span.ms-colon,
.time span.millisecond{
  color: #7D2Ae8;
}
.wrapper .buttons{
  text-align: center;
  margin-top: 20px;
}
.buttons button{
  padding: 6px 16px;
  outline: none;
  border: none;
  margin: 0 5px;
  color: #7D2Ae8;
  background: #fff;
  font-size: 19px;
  font-weight: 500;
  border-radius: 4px;
  cursor: pointer;
  box-shadow: 10px 10px 20px rgba(0,0,0,0.09);
}
.buttons button.active,
.buttons button.stopActive{
  pointer-events: none;
  opacity: 0.7;
}
</style>
<body>

  <div class="wrapper">
    <div class="time">
      <span class="hour">00</span>
      <span class="colon">:</span>
      <span class="minute">00</span>
      <span class="colon">:</span>
      <span class="second">00</span>
      <span class="colon ms-colon">:</span>
      <span class="millisecond">00</span>
    </div>
    <div class="buttons">
      <button class="start">Start</button>
      <button class="stop">Stop</button>
      <button class="reset">Reset</button>
    </div>
  </div>
  
  <script>
  let hr = min = sec = ms = "0" + 0,
    startTimer;
  const startBtn = document.querySelector(".start"),
   stopBtn = document.querySelector(".stop"),
   resetBtn = document.querySelector(".reset");
   startBtn.addEventListener("click", start);
   stopBtn.addEventListener("click", stop);
   resetBtn.addEventListener("click", reset);
  function start() {
    startBtn.classList.add("active");
    stopBtn.classList.remove("stopActive");
    startTimer = setInterval(()=>{
      ms++
      ms = ms < 10 ? "0" + ms : ms;
      if(ms == 100){
        sec++;
        sec = sec < 10 ? "0" + sec : sec;
        ms = "0" + 0;
      }
      if(sec == 60){
        min++;
        min = min < 10 ? "0" + min : min;
        sec = "0" + 0;
      }
      if(min == 60){
        hr++;
        hr = hr < 10 ? "0" + hr : hr;
        min = "0" + 0;
      }
      putValue();
    },10); //1000ms = 1s
  }
  function stop() {
    startBtn.classList.remove("active");
    stopBtn.classList.add("stopActive");
    clearInterval(startTimer);
  }
  function reset() {
    startBtn.classList.remove("active");
    stopBtn.classList.remove("stopActive");
    clearInterval(startTimer);
    hr = min = sec = ms = "0" + 0;
    putValue();
  }
  function putValue() {
    document.querySelector(".millisecond").innerText = ms;
    document.querySelector(".second").innerText = sec;
    document.querySelector(".minute").innerText = min;
    document.querySelector(".hour").innerText = hr;
  }
 </script>
</body>
</html>
