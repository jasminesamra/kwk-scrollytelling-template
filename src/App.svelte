<script>
  import LeftAlignedExample from "./sections/LeftAlignedExample.svelte";
  import RightAlignedExample from "./sections/RightAlignedExample.svelte";
  import ImageExample from "./sections/ImageExample.svelte";
  import TitleSection from "./sections/TitleSection.svelte";
  import InteresectionObserverBasicExample from "./sections/InteresectionObserverBasicExample.svelte";
  import IntersectionObserverAlertExample from "./sections/IntersectionObserverAlertExample.svelte";
  import DisappearingDuckExample from "./sections/DisappearingDuckExample.svelte";
  import IntersectionObserverSectionCard from "./sections/IntersectionObserverSectionCard.svelte";
  import IntersectionObserverListExample from "./sections/IntersectionObserverListExample.svelte";
  import MapExample from "./sections/MapExample.svelte";
  import EmbedMapExample from "./sections/EmbedMapExample.svelte";
  import TypewriterTitleSection from "./sections/TypewriterTitleSection.svelte";
</script>

<main>
  <TypewriterTitleSection/>
  <TitleSection />
  <EmbedMapExample />
  <!-- <MapExample /> -->
  <RightAlignedExample />
  <LeftAlignedExample />
  <ImageExample />

  <IntersectionObserverSectionCard />
  <InteresectionObserverBasicExample />
  <IntersectionObserverAlertExample />
  <DisappearingDuckExample />
  <IntersectionObserverListExample />
</main>
