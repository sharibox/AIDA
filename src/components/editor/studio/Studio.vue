// Studio.vue
// Component defines the studio; the interaction elements on the right side of
// the editor.
<template lang="html">
  <div class="pointers-please studioPanel elevation-2">

    <!-- The minimap naigation element -->
    <app-navigator/>

    <!-- Display and control annotation layers -->
    <app-layers/>

    <!-- Display and control images in the instance -->
    <app-images/>

    <!-- Display and control properties of the selected items -->
    <app-properties/>

    <!-- Display the validation history of the selected item -->
    <app-validations/>

  </div>

</template>

<script>
// Import child components
import navigator from './Navigator.vue'
import layers from './Layers.vue'
import images from './Images.vue'
import properties from './properties/Properties.vue'
import validations from './Validations.vue'

export default {
  components: {
    'app-navigator': navigator,
    'app-layers': layers,
    'app-images': images,
    'app-properties': properties,
    'app-validations': validations
  }
}
</script>
<style lang='css' scoped>
.studioPanel {
  background: #eeeeee;
  overflow: auto;
}
</style>
