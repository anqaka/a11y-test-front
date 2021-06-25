<template>
  <c-box>
    <c-flex direction="column">
      <result-element
        v-for="(item, id) in violations"
        :key="id"
        :item="item"
      />
    </c-flex>
  </c-box>
</template>

<script>
import { CBox, CFlex } from '@chakra-ui/vue'

export default {
  components: {
    CBox,
    CFlex
  },

  props: {
    violations: {
      type: Array,
      default: () => []
    }
  }
};
</script>
