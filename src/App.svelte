<script>
    import Main from "./lib/main/Main.svelte";
    import Question from "./lib/question/Question.svelte";
    import Result from "./lib/result/Result.svelte";

    import data from "./assets/data.js";

    let show = ["flex", "none", "none"];
    
    let score = [];
</script>

<main>
    <Main
        display={show[0]}
        on:start={() => {
            show[0] = "none";
            show[1] = "flex";
        }}
    />
    <Question
        display={show[1]}
        {data}
        on:result={(e) => {
            show[1] = "none";
            show[2] = "flex";
            score = e.detail.totalScore
        }}
    />
    <Result display={show[2]} {score}/>
</main>
