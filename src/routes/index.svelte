<script>
  import Fullpage from "svelte-fullpage/src/Fullpage.svelte";
  import FullpageSection from "svelte-fullpage/src/FullpageSection.svelte";
  import FullpageSlide from "svelte-fullpage/src/FullpageSlide.svelte";

  //Include all titles of your sections, this is also used as number that indicate count of sections
  const sections = ["Home", "History", "Present", "Future"];
  //Have to set to 0 (or section you wish to display as default), otherwise section will not display
  let activeSection = 0;

  //Same mechanics as in sections
  const slides = ["1982-1993", "1993-2006", "2006-present"];
  //Also has to be 0 or specific id of slide
  let activeSlide = 0;
</script>

<Fullpage bind:activeSection {sections} arrows>
  <FullpageSection sectionId="0" bind:activeSection center>
    ...Your markup here 1
  </FullpageSection>
  <FullpageSection
    sectionId="1"
    bind:activeSection
    bind:activeSlide
    {slides}
    arrows
    style="background-color: red;"
  >
    <FullpageSlide slideId="0" bind:activeSlide>
      ...Your markup here 2.1
    </FullpageSlide>
    <FullpageSlide slideId="1" bind:activeSlide>
      ...Your markup here 2.2
    </FullpageSlide>
    <FullpageSlide slideId="2" bind:activeSlide>
      ...Your markup here 2.3
    </FullpageSlide>
  </FullpageSection>
  <FullpageSection sectionId="2" bind:activeSection class="slide3">
    ...Your markup here 3
  </FullpageSection>
  <FullpageSection sectionId="3" bind:activeSection>
    ...Your markup here 4
  </FullpageSection>
</Fullpage>
