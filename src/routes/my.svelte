<script>
  import { fly } from "svelte/transition";
  import { elasticOut } from "svelte/easing";

  import Fullpage from "$lib/Fullpage.svelte";
  import Section from "$lib/Section.svelte";
</script>

<Fullpage click wheels>
  <Section name="primeira">
    <content
      class="content primeira"
      in:fly={{
        delay: 50,
        duration: 1500,
        x: -1500,
        y: 0,
        opacity: 0.5,
        easing: elasticOut,
      }}
    >
      <h2>Primeira</h2>
    </content>
  </Section>
  <Section name="segunda">
    <content
      class="content segunda"
      in:fly={{
        delay: 50,
        duration: 1500,
        x: -1500,
        y: 0,
        opacity: 0.5,
        easing: elasticOut,
      }}
    >
      <h2>Segunda</h2>
    </content>
  </Section>
  <Section name="terceira">
    <content class="content terceira">
      <h2>Terceira</h2>
    </content>
  </Section>
  <Section name="quarta">
    <content class="content">
      <h2>Quarta</h2>
    </content>
  </Section>
</Fullpage>

<style>
  .content {
    width: 100vw;
    min-height: 100vh;
  }

  .primeira {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: red;
  }

  .segunda {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: green;
  }

  .terceira {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: blue;
    animation: animationFrames ease 1s;
    animation-iteration-count: 1;
    transform-origin: 50% 50%;
    animation-fill-mode: forwards; /*when the spec is finished*/
  }

  @keyframes animationFrames {
    0% {
      opacity: 0;
      transform: translate(-1500px, 0px);
    }
    60% {
      opacity: 1;
      transform: translate(30px, 0px);
    }
    80% {
      transform: translate(-10px, 0px);
    }
    100% {
      opacity: 1;
      transform: translate(0px, 0px);
    }
  }
</style>
