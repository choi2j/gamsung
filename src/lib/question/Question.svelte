<script>
    export let data;
    export let display;

    import "./question.css";

    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    let no = 0;
    let stack = 1;

    let progress = 0;

    let redScore = 150,
        greenScore = 150,
        blueScore = 150;

    const addScore = (color, tag, idx, stack) => {
        if (color == "R") {
            if (tag == "P") {
                if (idx != 3) {
                    redScore += idx * 7 * stack;
                    stack += 0.5;
                } else {
                    redScore += idx;
                    stack = 1;
                }
            } else if (tag == "N") {
                if (idx != 3) {
                    redScore -= (6 - idx) * 3.5 * stack;
                    stack += 0.5;
                } else {
                    redScore += idx;
                    stack = 1;
                }
            }
        } else if (color == "G") {
            if (tag == "P") {
                if (idx != 3) {
                    greenScore += idx * 7 * stack;
                    stack += 0.5;
                } else {
                    greenScore += idx;
                    stack = 1;
                }
            } else if (tag == "N") {
                if (idx != 3) {
                    greenScore -= (6 - idx) * 3.5 * stack;
                    stack += 0.5;
                } else {
                    greenScore += idx;
                    stack = 1;
                }
            }
        } else if (color == "B") {
            if (tag == "P") {
                if (idx != 3) {
                    blueScore += idx * 7 * stack;
                    stack += 0.5;
                } else {
                    blueScore += idx;
                    stack = 1;
                }
            } else if (tag == "N") {
                if (idx != 3) {
                    blueScore -= (6 - idx) * 3.5 * stack;
                    stack += 0.5;
                } else {
                    blueScore += idx;
                    stack = 1;
                }
            }
        } else {
            if (idx != 3) {
                redScore += idx * 8 * stack;
                greenScore += idx * 8 * stack;
                blueScore += idx * 8 * stack;
            } else {
                redScore -= idx * 4 * stack;
                greenScore -= idx * 4 * stack;
                blueScore -= idx * 4 * stack;
            }
        }
    };

    const result = () => {
        dispatch("result", {
            question: "none",
            totalScore: [Math.floor(redScore), Math.floor(greenScore), Math.floor(blueScore)],
        });
    };
</script>

<div id="question-container" style:display>
    {#if no < data.length}
        <div id="slider" style:display>
            <div id="bar" style:padding-left={progress + "vw"} />
        </div>
    {/if}
    {#each data as d, idx}
        {#if idx != no && no < data.length}
            <div id="question" style:display={"none"} />
        {/if}
        {#if idx == no && no < data.length}
            <div id="question">
                <p id="number">no.{idx + 1}</p>
                <p id="question-q">{d.question}</p>
                <ul id="question-a">
                    {#each d.answers as a, i}
                        <li>
                            <button
                                on:click={() => {
                                    no += 1;
                                    addScore(d.color, d.tag, i + 1, stack);
                                    progress += 3;
                                }}>{i + 1}번. {a}</button
                            >
                        </li>
                    {/each}
                </ul>
            </div>
        {/if}
    {/each}
    {#if no == data.length}
        <button on:click={result} id="check">결과 확인하기</button>
    {/if}
</div>
