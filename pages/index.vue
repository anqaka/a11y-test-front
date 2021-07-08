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
        <c-box max-w="1280px" mx="auto">
          <app-form @submit="onSubmit" />
        </c-box>

        <c-box mt="10">
          <CHeading as="h2">
            {{ title }}
          </CHeading>
          <c-box d="flex" direction="row" justify-content="space-between" my="4">
            <CButton w="200px" @click="getResult">
              Get results
            </CButton>

            <CInputGroup>
              <CInputLeftElement>
                <CIcon name="search" color="gray.300" />
              </CInputLeftElement>
              <CInput v-model="search" placeholder="Search..." />
            </CInputGroup>
          </c-box>
          <results-list :title="result.title" :violations="violations" />
        </c-box>
      </c-box>
    </c-box>
    <scroll-to-top />
  </div>
</template>

<script lang="js">
import {
  CBox,
  CHeading,
  CButton,
  CInputGroup,
  CInput,
  CInputLeftElement,
  CIcon
} from '@chakra-ui/vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    CBox,
    CHeading,
    CButton,
    CInputGroup,
    CInput,
    CInputLeftElement,
    CIcon
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
      },
      search: '',
      result: {}
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
    },
    violations () {
      const violations = this.result.violations
      if (violations && violations.length && this.search) {
        return violations.filter((item) => {
          return Object.keys(item).some((key) => {
            return item[key].includes(this.search)
          })
        })
      }
      return this.result.violations
    },
    title () {
      return this.result.title ? `Results: ${this.result.title}` : 'Results'
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
      try {
        await axios({
          method: 'POST',
          url: `${process.env.axe}/axe`,
          data
        })
      } catch (e) {
        this.showToast(
          'Error',
          e.response.data ? error.response.data : 'Error occurred',
          'error'
        )
      }
    },

    async getResult () {
      try {
        const response = await axios({
          method: 'GET',
          url: `${process.env.axe}/axe`
        })
        this.result = response.data
      } catch (e) {
        this.showToast(
          'Error',
          e.response.data ? error.response.data : 'Error occurred',
          'error'
        )
      }
    }
  }
}
</script>
