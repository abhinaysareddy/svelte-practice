<script>
 import {Button} from 'sveltestrap';

 let count=0;
 let counter ;
 let display="00:00:00";
 let pause=false;
 let started=false;

 function padding(num){
    if(num<10)return "0"+num
    else return num+""
 }
 const startWatch=(event)=>{
   started=true;
   counter =  setInterval(()=>{
      if(!pause){
       count=count+1;
       var hrs=Math.floor(count/(60*60));
       var remainingSecs=count%(60*60);
       var mins=Math.floor(remainingSecs/60);
      var seconds=remainingSecs%60;
       display=padding(hrs)+":"+padding(mins)+":"+padding(seconds)
     }
    },1000);
 }
 const stopWatch=(event)=>{
   started=false;
    
   clearInterval(counter);
 }

 const pauseWatch=(event)=>{
   pause=!pause;
 }

</script>
<div class="box">
<h2>Stop Watch</h2>
<h1>{display}</h1>
{#if !started}
<Button on:click={startWatch} color={"primary"}  >Start

</Button>
<Button on:click={()=> {count=0}} color={"light"}  >Clear

</Button>
{/if}
{#if started}
<Button on:click={pauseWatch} color={"secondary"}  >{pause?'Continue':'Pause'}

</Button>
<Button on:click={stopWatch} color={"danger"}  >Stop

</Button>
{/if}
</div>