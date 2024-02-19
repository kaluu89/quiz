<script>
    import { onMount } from "svelte";
    export let question;
    export let correctAnswer;
    export let incorrectAnswers;
    const shuffle=(array)=>{return array.sort(()=>Math.random()-0.5)};
    $: possibleAnswers=shuffle([...incorrectAnswers,correctAnswer]);
    
    const handleCLick=(ans)=>{
        if(ans==correctAnswer){
            alert("Tacno!");
        }
        else{
            alert(`Netacan odgovor! Tacan je ${correctAnswer}`); 
        }
    }
    const getQuestion = async()=>{
        const res =await fetch('https://opentdb.com/api.php?amount=1&difficulty=easy&type=multiple');
        let data = await res.json();
        question=data.results[0].question;
        correctAnswer=data.results[0].correct_answer;
        incorrectAnswers=data.results[0].incorrect_answers;
        console.log(data)
    }
    onMount(getQuestion)
</script>

<div>
    <h3>{@html question}</h3>
    <div id="answers">
        {#each possibleAnswers as pa,i}
        <button on:click={()=>handleCLick(pa)}>{pa}</button>
        {/each}
    </div>
</div>