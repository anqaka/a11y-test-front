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
      <c-box
        :w="['100vw', '30vw']"
        boxShadow=" 0 4px 6px 0 rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)"
        p="10"
        mr="10"
      >
        <app-form @submit="onSubmit" />
      </c-box>
    </c-box>
  </div>
</template>

<script lang="js">
import {
  CBox,
  CHeading
} from '@chakra-ui/vue'

export default {
  name: 'App',
  components: {
    CBox,
    CHeading
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
