<template>
  <c-box fontSize="sm" my="2">
    <c-box pb="2">
      <CText fontSize="sm" fontWeight="800">Any</CText>
      <pre style="white-space: break-spaces;">{{ any }}</pre>
    </c-box>
    <c-box pb="2">
      <CText fontSize="sm" fontWeight="800">All</CText>
      <pre style="white-space: break-spaces;">{{ all }}</pre>
    </c-box>
    <c-box pb="2">
      <CText fontSize="sm" fontWeight="800">None</CText>
      <pre style="white-space: break-spaces;">{{ none }}</pre>
    </c-box>
    <c-box pb="2">
      <CText fontSize="sm" fontWeight="800">Html</CText>
      <pre style="white-space: break-spaces;">{{ html }}</pre>
    </c-box>
    <c-box pb="2" v-if="target">
      <CText fontSize="sm" fontWeight="800">Target</CText>
      <pre style="white-space: break-spaces;">{{ target.join(", ") }}</pre>
    </c-box>
  </c-box>
</template>

<script>
import {
  CBox,
  CText
} from '@chakra-ui/vue'

export default {
  components: {
    CBox,
    CText
  },
  props: {
    any: {
      type: Array
    },
    all: {
      type: Array
    },
    none: {
      type: Array
    },
    html: {
      type: String
    },
    target: {
      type: Array
    }
  }
}
</script>
