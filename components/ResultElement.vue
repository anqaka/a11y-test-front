<template>
  <c-box
    boxShadow=" 0 4px 6px 0 rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)"
    mb="4"
  >
    <CSimpleGrid :columns="[1, null, 3, 5]" mb="4" p="4" bg="gray.200">
      <c-box>
        <CText fontSize="sm">Id</CText>
        <CText fontWeight="800" py="2">{{ item.uid || item.id }}</CText>
      </c-box>
      <c-box>
        <CText fontSize="sm">Tested Url</CText>
        <CText fontWeight="800" py="2" is-truncated>
          {{ item.testedUrl }}
        </CText>
      </c-box>
      <c-box>
        <CText fontSize="sm">Category</CText>
        <CText fontWeight="800" py="2"> {{ item.category }}</CText>
      </c-box>
      <c-box>
        <CText fontSize="sm">Impact</CText>
        <CText fontWeight="800" py="2"> {{ item.impact }}</CText>
      </c-box>
      <c-box>
        <CText fontSize="sm">Status</CText>
        <CText fontWeight="800">
          {{ item.status }}
        </CText>
      </c-box>
    </CSimpleGrid>

    <c-box p="4">
      <c-grid
        :template-columns="['repeat(1, 1fr)', null, null, 'repeat(12, 1fr)']"
        pb="2"
      >
        <c-grid-item col-span="1">
          <CText>Tags:</CText>
        </c-grid-item>
        <c-grid-item col-span="11">
          <CText fontSize="sm">{{ item.tags.join(", ") }}</CText>
        </c-grid-item>
      </c-grid>
      <c-grid
        :template-columns="['repeat(1, 1fr)', null, null, 'repeat(12, 1fr)']"
        pb="2"
      >
        <c-grid-item col-span="1">
          <CText>Description:</CText>
        </c-grid-item>
        <c-grid-item col-span="11">
          <CText fontSize="sm"> {{ item.description }}</CText>
        </c-grid-item>
      </c-grid>
      <c-grid
        :template-columns="['repeat(1, 1fr)', null, null, 'repeat(12, 1fr)']"
        pb="2"
      >
        <c-grid-item col-span="1">
          <CText>Help:</CText>
        </c-grid-item>
        <c-grid-item col-span="11">
          <CText fontSize="sm"> {{ item.help }}</CText>
        </c-grid-item>
      </c-grid>
      <c-grid
        :template-columns="['repeat(1, 1fr)', null, null, 'repeat(12, 1fr)']"
        pb="2"
      >
        <c-grid-item col-span="1">
          <CText>Help Url:</CText>
        </c-grid-item>
        <c-grid-item col-span="11">
          <CLink
            fontSize="sm"
            :href="item.helpUrl"
            color="blue.400"
            is-external
          >
            {{ item.helpUrl }}
          </CLink>
        </c-grid-item>
      </c-grid>
    </c-box>

    <c-box p="4">
      <node-element
        v-if="item && !item.nodes"
        :any="item.any"
        :all="item.all"
        :none="item.none"
        :html="item.html"
        :target="item.target"
      />

      <template v-else-if="item && item.nodes.length">
        <c-box v-for="(node, id) in item.nodes" :key="id">
          <node-element
            :any="node.any"
            :all="node.all"
            :none="node.none"
            :html="node.html"
            :target="node.target"
          />
          <CDivider />
        </c-box>
      </template>
    </c-box>
  </c-box>
</template>

<script>
import {
  CBox,
  CSimpleGrid,
  CText,
  CLink,
  CGrid,
  CGridItem,
  CDivider
} from '@chakra-ui/vue'

export default {
  components: {
    CBox,
    CSimpleGrid,
    CText,
    CLink,
    CGrid,
    CGridItem,
    CDivider
  },

  props: {
    item: {
      type: Object,
      default: () => {}
    }
  },

  data () {
    return {
      show: false
    }
  }
}
</script>
