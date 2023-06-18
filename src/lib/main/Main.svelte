<script>
    export let display;

    import Fa from "svelte-fa";
    import { faGithub, faInstagram } from "@fortawesome/free-brands-svg-icons";

    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    import "./main.css";

    let help = "none";

    const start = () => {
        dispatch("start", {
            main: "none",
        });
    };
</script>

<div id="main" style:display>
    <div id="intro">
        <p>Gamsung</p>
    </div>

    <button id="start" on:click={start}>테스트 시작</button>

    <button
        id="help"
        on:click={() => {
            help = "flex";
        }}>도움말</button
    >

    <div id="help-container" style:display={help}>
        <div id="help-info">
            <p><span>Gamsung</span>은 약간의 테스트를 통해 당신의 감정에 맞는 색을 찾아주는 서비스입니다.</p>
            <p>물론 이 결과는 정확하지 않을 확률이 높고 전문성이 없기에 재미로만 봐주세요.</p>
            <button
                on:click={() => {
                    help = "none";
                }}>창 닫기</button
            >
        </div>
    </div>

    <div id="contact">
        <p>Sunrin Hackathon Project</p>
        <a href="https://www.github.com/choi2j">
            <Fa icon={faGithub} />
        </a>
        <a href="https://www.instagram.com/choi2j86">
            <Fa icon={faInstagram} />
        </a>
    </div>
</div>
