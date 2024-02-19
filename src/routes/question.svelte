<script>
    export let question;
    export let correctAnswer;
    export let incorrectAnswers;
    const shuffle=(array)=>{return array.sort(()=>Math.random()-0.5)};
    let possibleAnswers=shuffle([...incorrectAnswers,correctAnswer]);
    
    const handleCLick=(ans)=>{
        if(ans==correctAnswer){
            alert("Tacno!");
        }
        else{
            alert(`Netacan odgovor! Tacan je ${correctAnswer}`); 
        }
    }
</script>

<div>
    <h3>{@html question}</h3>
    <div id="answers">
        {#each possibleAnswers as pa,i}
        <button on:click={()=>handleCLick(pa)}>{pa}</button>
        {/each}
    </div>
</div>