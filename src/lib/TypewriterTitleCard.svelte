<script>
    import { onMount } from "svelte";

    let { title, subtitle } = $props();
    let visible = $state(false);

    function typewriter(node, { speed = 1 }) {
        const valid =
            node.childNodes.length === 1 &&
            node.childNodes[0].nodeType === Node.TEXT_NODE;

        if (!valid) {
            throw new Error(
                `This transition only works on elements with a single text node child`,
            );
        }

        const text = node.textContent;
        const duration = text.length / (speed * 0.01);

        return {
            duration,
            tick: (t) => {
                const i = Math.trunc(text.length * t);
                node.textContent = text.slice(0, i);
            },
        };
    }

    onMount(() => {
        visible = !visible;
    });
</script>

<div class="title-card">
    <div class="content">
        {#if visible}
            <h1
                transition:typewriter
                onintroend={() => (visible = !visible)}
                onoutroend={() => (visible = !visible)}
            >
                {title}
            </h1>
        {/if}
        <p>{subtitle}</p>
    </div>
</div>

<style>
    .title-card {
        background-color: #007052;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        padding: 2rem;
        box-sizing: border-box;
        font-family: "Inter", sans-serif;
    }

    .content {
        max-width: 700px;
        background-color: #034c36;
        padding: 2rem;
        border: 6px solid #e3ff00;
        border-radius: 2rem;
        box-shadow: 16px 16px #188f70;
    }

    h1 {
        font-size: 3rem;
        margin: 0;
        color: #e3ff00;
        text-shadow: 1px 1px 0 #007052;
    }

    p {
        font-size: 1.3rem;
        color: #f7f5eb;
        margin-top: 1rem;
    }

    @media (max-width: 600px) {
        h1 {
            font-size: 2.2rem;
        }

        p {
            font-size: 1.1rem;
        }
    }
</style>
