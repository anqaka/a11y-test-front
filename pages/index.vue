<template>
  <div class="container">
    <c-box
      v-bind="mainStyles[colorMode]"
      d="flex"
      w="100vw"
      h="100vh"
      my="10"
      flex-dir="column"
    >
      <CHeading text-align="center" mb="4">
        A11y testing with axe
      </CHeading>
      <c-box m="10">
        <c-box
          mr="10"
        >
          <app-form @submit="onSubmit" />
        </c-box>
        <c-box mt="10">
          <CButton @click="getResult">
            Results
          </CButton>
          <results-list :result="result" />
        </c-box>
      </c-box>
    </c-box>
  </div>
</template>

<script lang="js">
import {
  CBox,
  CHeading,
  CButton
} from '@chakra-ui/vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    CBox,
    CHeading,
    CButton
  },

  inject: ['$chakraColorMode', '$toggleColorMode'],

  data () {
    return {
      showModal: false,
      mainStyles: {
        dark: {
          bg: 'gray.700',
          color: 'whiteAlpha.900'
        },
        light: {
          bg: 'white',
          color: 'gray.900'
        }
      }
    }
  },
  computed: {
    colorMode () {
      return this.$chakraColorMode()
    },
    theme () {
      return this.$chakraTheme()
    },
    toggleColorMode () {
      return this.$toggleColorMode
    }
  },
  methods: {
    showToast (title, message, status = 'success') {
      this.$toast({
        title,
        description: message,
        status,
        duration: 10000,
        isClosable: true
      })
    },

    async onSubmit (data) {
      // todo
    }
  }
}
</script>
