<template>
    <div>
        <link rel="stylesheet" href="https://unpkg.com/@lottiefiles/lottie-interactivity@latest/dist/lottie-interactivity.min.js">
          <link href="https://fonts.googleapis.com/css2?family=Kurale&family=Mulish:wght@700&family=Merriweather+Sans:ital,wght@1,600&family=Libre+Baskerville&family=Brygada+1918:ital,wght@1,500&family=Montserrat+Alternates:wght@500&display=swap" rel="stylesheet">
           <link href="https://fonts.googleapis.com/css2?family=Allerta&family=Julius+Sans+One&family=El+Messiri:wght@700&family=Montserrat+Alternates:wght@500&display=swap" rel="stylesheet">
          
           <h1> QUIZ APP</h1>
           
        <div class="question-section">
                <img  v-if="showSection===false" class="welcome" src='./assets/welcome (1).gif'>
                <img v-if="showSection===false" class="start-btn" @click="showSection =!showSection" src='./assets/start-button.gif' alt="">
                
        <div v-if="showSection" class="answer-part">
               <h5>Question {{index}}/{{count}}</h5>
               <img style="position:absolute; width:100px;height:100px;margin-left:16rem;
                            margin-top:-5rem;" src='./assets/timer.gif'>
            <div v-if="index < count">   
               <div  class="quesstion-text"> <h3> {{questions[index]['questionText']}} </h3> </div>
                 
                    <label :for="key" 
                         class="answer-section"
                         v-for="answerOption,key in  questions[index] ['answerOptions']" :key="answerOption" 
                        :class="{
                            'label' : selectedAnswer =='',
                            'r-ans' : selectedAnswer != questions[index]['correctAnswer'] && selectedAnswer ==key,
                            'c-ans': key == questions[index]['correctAnswer'] && selectedAnswer !=''
                            }"
                            
                     > 
                
                    <input class="hidden"
                      type="radio" 
                      v-model="selectedAnswer"
                      :id="key"
                      :value="key"
                      @change="answered($event)"
                      :disabled="selectedAnswer !=''"
                     />
                
                 <h6>  {{answerOption}} </h6>   
                
               </label>
            
            <div>
                
                    <button class="nxt-btn " v-show="selectedAnswer !='' && index < count-1"
                                @click="nextQuestion">Next </button>
                    <button class="nxt-btn " v-show="selectedAnswer !='' && index == count-1"
                                @click="showResults">Finish</button>
                    
            </div>
          
         </div>
      
             
                <div  class="result-page" v-else >
                    <div  class="result">
                        <img v-show="correctAnswer === count" src='./assets/excellent.gif' alt="">
                        <img v-show="correctAnswer === count-1" src='./assets/well-done.gif' alt="">
                        <h2 class="score">Results</h2>
                        <p class="t-score"> You got <span style="font-size:23px;color:green;">{{correctAnswer}}</span> correct answer</p>
                            <button  class="play-again" @click="resetQuiz">Play again</button>
                        </div>
                </div>
           </div>

       </div>
   </div>
</template>

<script>

    export default {
        data(){
            return{
                showResult:false,
                showScore:false,
                showSection:false,
                index:0,
                selectedAnswer:'',
                count:11,
                correctAnswer:0,
                question:0,
               questions:[
                {
                       questionText:'Which is the capital of India?',
                        answerOptions: 
                        {a:'a. Chennai',b:'b. Hydrabad',c:'c. Mumbai', d:'d. New Delhi'},
                        correctAnswer:'d'

                },
                {
                       questionText:'Which is the capital Chaina ?',
                        answerOptions: 
                        {a:'a. Hong kong',b:'b. Shanghai', c:'c. Beijing',d:'d. France'},
                        correctAnswer:'c'

                },
                       {
                       questionText:'Which is the capital France ?',
                        answerOptions: 
                        {a:'a. Paris',b:'b. London', c:'c. Brazil',d:'d. Tokiyo'},
                        correctAnswer:'a'

                },
                       {
                       questionText:'Which is the capital Canada ?',
                        answerOptions: 
                        {a:'a.Ottawa',b:'b. Toronto', c:'c. Vancouver',d:'d. France'},
                        correctAnswer:'a'

                },
                       {
                       questionText:'Which is the capital Australia ?',
                        answerOptions: 
                        {a:'a. Canberra',b:'b. Melbourne', c:'c. France',d:'d. Sydney'},
                        correctAnswer:'d'

                },
                       {
                       questionText:'Which is the capital United Kingdom ?',
                        answerOptions: 
                        {a:'a. Hong kong',b:'b. London', c:'c. Beijing',d:'d. France'},
                        correctAnswer:'b'

                },
                       {
                       questionText:'Which is the capital Iran ?',
                        answerOptions: 
                        {a:'a.Baghdad ',b:'b. Kabul', c:'c. Tehran',d:'d. France'},
                        correctAnswer:'c'

                },
                       {
                       questionText:'Which is the capital Italy ?',
                        answerOptions: 
                        {a:'a. Rome',b:'b. England', c:'c. Narway',d:'d. France'},
                        correctAnswer:'a'

                },
                       {
                       questionText:'Which is the capital Japan ?',
                        answerOptions: 
                        {a:'a. Hong kong',b:'b. Tokyo', c:'c. Beijing',d:'d. France'},
                        correctAnswer:'b'

                },
                       {
                       questionText:'Which is the capital United States ?',
                        answerOptions: 
                        {a:'a. Hong kong',b:'b. America', c:'c. Washington',d:'d. France'},
                        correctAnswer:'c'

                },

                  {
                       questionText:'Which is the capital Russia ?',
                        answerOptions: 
                        {a:'a. Novosibirsk',b:'b. Moscow', c:'c. Saint Petersburg',d:'d. Krasnodar'},
                        correctAnswer:'b'

                },
                
                   
                   
            ],

        }
    },
    methods:{
        answered(e){
             this.selectedAnswer = e.target.value
             if(this.selectedAnswer == this.questions[this.index]['correctAnswer'])
             this.correctAnswer++
             else 
             this.wrongAnswer++
             console.log(this.correctAnswer+""+this.wrongAnswer)
        },
        nextQuestion(){
            this.index++
            this.selectedAnswer =''
        },
        showResults(){
            this.index++
        },
        resetQuiz(){
            this.index=0
            this.selectedAnswer=''
            this.correctAnswer=0
            this.wrongAnswer=0
        }
     
    }
}
</script>

<style>
body{
    align-items: center;
    margin:0;
    padding:0;
    position:relative;
    display:flex;
}
h1{
 margin-left:31rem;
 font-size:20px;
 margin-top:5rem;
 font-weight:700;
font-family: 'Libre Baskerville', serif;

}
.question-section{
    border-radius: 10px;
    box-shadow:6px 6px 35px -11px rgba(0, 0, 0, 0.95);
    cursor:pointer;
    width:500px;
    height:480px;
    display:flex;
    margin-top:1rem;
    margin-left:30rem;
    align-items: center;
    position: absolute;
    
}

.question-section > .welcome{
    width:400px;
    height:400px;
    text-align: center;
    margin-top:-15rem;
    margin-left:4rem;
    z-index:-1;
    background: transparent;
}
.start-btn{
    width:200px;
    height:200px;
    margin-top:6rem;
    position:absolute;
    align-items:center;
    margin-left:9rem;

}
.hidden{
    display:none;
}
h6{
    font-size:16px;
    text-align: left;
    margin-top:0.5rem;
    margin-left:5rem;
    font-weight:400;
    transition:transform 100ms ease-in;
    font-family: 'Allerta', sans-serif;

}


h3{
    font-size:18px;
    margin-top:-1rem;
    margin-left:-4rem;
    font-family: 'El Messiri', sans-serif;
    text-align: left;
    
}
h5{
    text-align: center;
    font-size:20px;
    font-weight:600;
    margin-left:1rem;
    position:absolute;
    text-align:left;
    margin-top:-5rem;
    font-family: 'Brygada 1918', serif;
   
}
.answer-section{
      width:250px;
      height:40px;
      border:0.5px solid gray;
      display:block;
      margin-top:1.5rem;
      position:relative;
      border-radius:5px;
      margin-left:-4rem;
      transition:transform 100ms ease-in;
    
}
.answer-section{
      transform:scale(1.07);
}
label:hover > h6{
    color:white;
    transform:scale(1.07);
}
.label:hover{
  background:orange;
  cursor:pointer; 

}
.c-ans{
    background: rgb(1, 184, 1);
}
.r-ans{
    background:rgb(231, 14, 14);
}
.answer-part{
    position:absolute;
    top:7rem;
    left:8rem;
}
.nxt-btn{
    float:right;
    background:rgb(122, 11, 212);
    padding:10px 25px;
    margin-left:15rem;
    border-radius:15px;
    font-size:18px;
    border:none;
    font-family: 'Kurale', serif;
    transition:transform 100ms ease-in;
    box-shadow:6px 6px 35px -11px rgba(0, 0, 0, 0.95);
}
.nxt-btn:hover{
    background: #fff;
    color:rgb(70, 0, 128);
    transform: scale(1.07);

}
.play-again{
    transition:transform 100ms ease-in;
    box-shadow:6px 6px 35px -11px rgba(0, 0, 0, 0.95);
    background:rgb(122, 11, 212);
    padding:10px 25px;
    border-radius:15px;
    font-size:15px;
    border:none;
    font-weight:bold;
    width:140px;
    height:40px;
    align-items: center;
    margin-top:2rem;
    margin-left:9.5rem;
    font-family: 'Kurale', serif;
 
}
.play-again:hover{
     background: #fff;
    color:rgb(70, 0, 128);
    transform: scale(1.07);

}
.result-page{
    position:absolute;
    margin-top:-9rem;
    margin-left:-6rem;
}
.result{
    position:absolute;
}
.result > img{
    width:480px;
    height:350px;
    margin-left:-1rem;
    margin-top:2rem;

}

.score{
    margin-top:-20rem;
    font-size:25px;
    color:#060c2c;
    text-align:left;
    transition:transform 100ms ease-in;
    font-family: 'Merriweather Sans', sans-serif;
}
.score:hover{
     transform: scale(1.07);
}
.t-score{
    margin-top:16rem;
    text-align: center;
    font-weight:700;
    font-family: 'Mulish', sans-serif;
}

</style>