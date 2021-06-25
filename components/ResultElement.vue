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
      <c-box fontSize="sm" my="2">
        <c-box pb="2">
          <CText fontSize="sm" fontWeight="800">Any</CText>
          <pre style="white-space: break-spaces;">{{ item.any }}</pre>
        </c-box>
        <c-box pb="2">
          <CText fontSize="sm" fontWeight="800">All</CText>
          <pre style="white-space: break-spaces;">{{ item.all }}</pre>
        </c-box>
        <c-box pb="2">
          <CText fontSize="sm" fontWeight="800">None</CText>
          <pre style="white-space: break-spaces;">{{ item.none }}</pre>
        </c-box>
        <c-box pb="2">
          <CText fontSize="sm" fontWeight="800">Html</CText>
          <pre style="white-space: break-spaces;">{{ item.html }}</pre>
        </c-box>
        <c-box pb="2" v-if="item.target">
          <CText fontSize="sm" fontWeight="800">Target</CText>
          <pre style="white-space: break-spaces;">{{ item.target.join(', ') }}</pre>
        </c-box>
      </c-box>
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
  CGridItem
} from '@chakra-ui/vue'

export default {
  components: {
    CBox,
    CSimpleGrid,
    CText,
    CLink,
    CGrid,
    CGridItem
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
