<script>
    import { fade, fly, scale } from "svelte/transition";
    import Scroller from "../lib/Scroller.svelte";
    import ObservedArticleText from "../lib/ObservedArticleText.svelte";

    let duckIsVisible = $state(false);

    const options = {
        threshold: [0.85, 0.95],
    };

    const simpleCallback = (entries, observer) => {
        entries.forEach((entry) => {
            const elem = entry.target;

            if (entry.intersectionRatio >= 0.9) {
                // "active" state
                elem.style.backgroundColor = "#e3ff00";
            } else if (entry.intersectionRatio < 0.9) {
                // "inactive" state
                elem.style.backgroundColor = "#888888";
            }
        });
    };

    const showDuckCallback = (entries, observer) => {
        entries.forEach((entry) => {
            const elem = entry.target;

            if (entry.intersectionRatio >= 0.9) {
                elem.style.backgroundColor = "#e3ff00";
                duckIsVisible = true;
            } else if (entry.intersectionRatio < 0.9) {
                elem.style.backgroundColor = "#888888";
            }
        });
    };

    const removeDuckCallback = (entries, observer) => {
        entries.forEach((entry) => {
            const elem = entry.target;

            if (entry.intersectionRatio >= 0.9) {
                elem.style.backgroundColor = "#e3ff00";
                duckIsVisible = false;
            } else if (entry.intersectionRatio < 0.9) {
                elem.style.backgroundColor = "#888888";
            }
        });
    };
</script>

<div>
    <Scroller layout="left">
        {#snippet sticky()}
            <div>
                {#if duckIsVisible}
                    <img
                        class="duck-img"
                        src="duck.png"
                        alt="KWK rubber duck!"
                        in:scale
                        out:fade={{ duration: 2000 }}
                    />
                {:else}
                <img
                        class="kwk-img"
                        src="kwk.png"
                        alt="KWK rubber duck!"
                        in:scale
                        out:fade={{ duration: 2000 }}
                    />
                {/if}
                <br />
                     <img
                        class="kwk-img"
                        src="kwk.png"
                        alt="KWK rubber duck!"
                        in:scale
                        out:fade={{ duration: 2000 }}
                    />
            </div>
        {/snippet}

        {#snippet scrolly()}
            <ObservedArticleText callback={removeDuckCallback} {options}>
                This example shows how to use an Intersection Observer callback
                along with a <a href="https://svelte.dev/docs/svelte/transition"
                    >Svelte transition.</a
                >
                <br /><br />
                Svelte transitions are built-in, easy to use animations that elevate
                the user experience as elements change on the website. Try them out
                in the tutorial
                <a href="https://svelte.dev/tutorial/svelte/transition">here</a>
                (and the next few pages).
                <br /><br />
                You can also
                <a
                    href="https://svelte.dev/tutorial/svelte/custom-css-transitions"
                >
                    build your own transitions
                </a> (it's not as hard as you think!).
            </ObservedArticleText>

            <ObservedArticleText callback={showDuckCallback} {options}>
                When this box scrolls into view, the callback will set a boolean
                variable, <code>duckIsVisible</code> to
                <code>true</code>.
                <br /><br />
                Because <code>duckIsVisible</code> is declared as
                <a href="https://svelte.dev/tutorial/svelte/state"> state</a>
                , and the duck image is only rendered conditionally if
                <code>duckIsVisible==true</code>, Svelte automatically updates
                the page and adds the duck component.
                <br /><br />
                The svelte transition
                <code>{"in:fly={{ y: 200, duration: 2000 }}"}</code>
                handles <strong>animating</strong> the transition.
            </ObservedArticleText>

            <ObservedArticleText callback={removeDuckCallback} {options}>
                When this box scrolls into view, the callback will set
                <code>duckIsVisible</code> to <code>false</code>.
                <br /><br />
                Svelte then automatically updates the page (more precisely, the DOM)
                and removes the duck component.
                <br /><br />
                The Svelte transition
                <code>{"out:fade"}</code>
                handles animating the transition.
            </ObservedArticleText>

            <ObservedArticleText callback={simpleCallback} {options}>
                Pretty slick, huh?
                <br /><br />
                🤔
                <strong
                    >How might you use a transition like this for emotional
                    impact in your final project?</strong
                >
            </ObservedArticleText>
        {/snippet}
    </Scroller>
</div>

<style>
    .duck-img {
        margin: 0px auto;
    }
    .kwk-img {
        width: 100px;
    }
</style>
