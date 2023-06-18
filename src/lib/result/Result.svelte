<script>
    import "./result.css";

    export let display;
    export let score;

    score.forEach((e) => {
        if (e > 255) {
            e = 255;
        } else if (e < 0) {
            e = 0;
        }
    });
</script>

<div id="result" style:display style="--color1: rgb({score[0]}, {score[1]}, {score[2]});">
    <p id="res">결과</p>
    <p id="color">RED : {score[0]} | GREEN : {score[1]} | BLUE : {score[2]}
    <br/> rgb({score})
    </p>
    <div id="screen" />
    <p>주의사항 : 점수 계산에는 랜덤요소가 들어가있으므로 매번 결과가 같지 않을 수 있습니다!</p>
    <a href="/">다시하기</a>
</div>

<style scoped>
    #screen {
        background-color: var(--color1);
    }
</style>
