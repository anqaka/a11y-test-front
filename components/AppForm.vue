<template>
  <CBox
    boxShadow="0 4px 6px 0 rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)"
    p="10"
  >
    <form @submit.prevent>
      <!-- Pages config -->
      <CBox my="4" pb="6">
        <CHeading as="h2" size="sm" pt="4">
          Pages
        </CHeading>
        <CDivider />
        <CBox
          v-for="(item, index) in form.pages"
          :key="index"
          d="flex"
        >
          <CFlex
            justify="flex-end"
            wrap="wrap"
            w="100%"
          >
            <CFormControl
              py="2"
              :isRequired="index === 0"
              w="100%"
            >
              <CFormLabel :for="`url-${index}`">
                Url
              </CFormLabel>
              <CInput
                :id="`url-${index}`"
                v-model="form.pages[index].url"
                placeholder="url"
                :name="`url-${index}`"
              />
            </CFormControl>
            <CFormControl py="2" :w="['100%', null, '50%']">
              <CFormLabel :for="`selector-${index}`">
                HTML selector
              </CFormLabel>
              <CInput
                :id="`selector-${index}`"
                v-model="form.pages[index].selector"
                placeholder="HTML selector"
                :name="`selector-${index}`"
              />
              <CFormHelperText>
                use .class or #id to choose selector to test, just one selector allowed. If empty whole document will be tested.
              </CFormHelperText>
            </CFormControl>
          </CFlex>
          <CButton
            v-if="index !== 0"
            mt="10"
            mx="4"
            @click="removePage"
          >
            Remove page
          </CButton>
        </CBox>
        <CButton @click="addPage">
          Add another page
        </CButton>
      </CBox>

      <!-- General config -->
      <CFlex :wrap="['wrap', null, 'nowrap']" justify="space-between">
        <CHeading as="h2" size="sm" pt="4" :width="['100%', null, 'auto']">
          General
        </CHeading>
        <CButton
          variant-color="blue"
          :width="['100%', null, 'auto']"
          @click="generalShow = !generalShow"
        >
          Toggle
        </CButton>
      </CFlex>
      <CDivider />
      <CCollapse :is-open="generalShow">
        <CSimpleGrid :columns="[1, null, 2]" spacing-x="40px">
          <CFormControl py="2">
            <CFormLabel for="title">
              Audit title
            </CFormLabel>
            <CInput
              id="title"
              v-model="form.title"
              placeholder="Title"
            />
          </CFormControl>
          <CFormControl py="2">
            <CFormLabel for="fileName">
              Export filename
            </CFormLabel>
            <CInput
              id="fileName"
              v-model="form.fileName"
              placeholder="Filename"
            />
          </CFormControl>
          <CFormControl py="2">
            <CFormLabel for="resultsDir">
              Results dir
            </CFormLabel>
            <CInput
              id="resultsDir"
              v-model="form.resultsDir"
              placeholder="Result directory name"
            />
          </CFormControl>
        </CSimpleGrid>
      </CCollapse>

      <!-- Axe options config -->
      <CFlex :wrap="['wrap', null, 'nowrap']" justify="space-between">
        <CHeading as="h2" size="sm" pt="4" :width="['100%', null, 'auto']">
          Axe Config
        </CHeading>
        <CButton
          variant-color="blue"
          :width="['100%', null, 'auto']"
          @click="axeConfigShow = !axeConfigShow"
        >
          Toggle
        </CButton>
      </CFlex>
      <CDivider />
      <CCollapse :is-open="axeConfigShow">
        <CSimpleGrid :columns="[1, null, 2]" spacing-x="40px">
          <CFormControl py="2">
            <CFormLabel for="reporter">
              Reporter
            </CFormLabel>
            <CInput
              id="reporter"
              v-model="form.axeConfig.reporter"
              placeholder="Reporter"
            />
          </CFormControl>
        </CSimpleGrid>

        <CHeading as="h2" size="sm" pt="4">
          Viewport
        </CHeading>
        <CDivider />
        <CSimpleGrid :columns="[1, null, 2]" spacing-x="40px">
          <CFormControl py="2">
            <CFormLabel for="width">
              Width (px)
            </CFormLabel>
            <CInput
              id="width"
              v-model="form.viewport.width"
              type="number"
              placeholder="Width"
            />
          </CFormControl>
          <CFormControl py="2">
            <CFormLabel for="height">
              Height (px)
            </CFormLabel>
            <CInput
              id="height"
              v-model="form.viewport.height"
              type="number"
              placeholder="Height"
            />
          </CFormControl>
        </CSimpleGrid>
      </CCollapse>

      <!-- BAsic auth config -->
      <CFlex :wrap="['wrap', null, 'nowrap']" justify="space-between">
        <CHeading as="h2" size="sm" pt="4" :width="['100%', null, 'auto']">
          Basic Auth configuration
        </CHeading>
        <CButton
          variant-color="blue"
          :width="['100%', null, 'auto']"
          :mt="[4, 0]"
          @click="basicAuthShow = !basicAuthShow"
        >
          Toggle
        </CButton>
      </CFlex>
      <CDivider />
      <CCollapse :is-open="basicAuthShow">
        <CSimpleGrid :columns="[1, null, 2]" spacing-x="40px">
          <CFormControl py="2">
            <CFormLabel for="username">
              Username
            </CFormLabel>
            <CInput
              id="username"
              v-model="form.basicAuth.username"
              placeholder="Username"
            />
          </CFormControl>
          <CFormControl py="2">
            <CFormLabel for="password">
              Password
            </CFormLabel>
            <CInput
              id="password"
              v-model="form.basicAuth.password"
              type="password"
              placeholder="Password"
            />
          </CFormControl>
        </CSimpleGrid>
      </CCollapse>

      <CSimpleGrid :columns="[1, null, 2]" spacing-x="40px">
        <CButton
          mt="2"
          variant-color="blue"
          :disabled="disabled"
          @click="onSubmit"
        >
          Send
        </CButton>
      </CSimpleGrid>
    </form>
  </CBox>
</template>

<script>
import {
  CBox,
  CFormControl,
  CFormLabel,
  CInput,
  CFormHelperText,
  CDivider,
  CHeading,
  CButton,
  CSimpleGrid
} from '@chakra-ui/vue'

export default {
  components: {
    CBox,
    CFormControl,
    CFormLabel,
    CFormHelperText,
    CInput,
    CDivider,
    CHeading,
    CButton,
    CSimpleGrid
  },

  data () {
    return {
      form: {
        pages: [
          {
            url: null,
            selector: null
          }
        ],
        title: undefined,
        fileName: undefined,
        resultsDir: undefined,
        basicAuth: {
          username: null,
          password: null
        },
        axeConfig: {
          reporter: null
        },
        viewport: {
          width: null,
          height: null
        }
      },
      generalShow: true,
      axeConfigShow: false,
      basicAuthShow: false
    }
  },

  computed: {
    disabled () {
      return (
        !this.form.pages
      )
    }
  },

  methods: {
    onSubmit () {
      const form = this.form
      const data = {
        ...form,
        // pages: form.pages || undefined,
        // title: form.title || undefined,
        // fileName: form.fileName || undefined,
        // resultsDir: form.resultsDir || undefined,
        basicAuth:
          form.basicAuth.username && form.basicAuth.password
            ? form.basicAuth
            : undefined,
        axeConfig: form.axeConfig.reporter ? form.axeConfig : undefined,
        viewport:
          form.viewport.width && form.viewport.height
            ? form.viewport
            : undefined
      }
      // console.log(data)
      this.$emit('submit', data)
      // this.clear()
    },

    addPage () {
      this.form.pages.push({ url: null, selector: null })
    },

    removePage () {
      this.form.pages.pop()
    },

    clear () {
      this.form = {
        pages: [
          {
            url: null,
            selector: null
          }
        ],
        title: undefined,
        fileName: undefined,
        resultsDir: undefined,
        basicAuth: {
          username: null,
          password: null
        },
        axeConfig: {
          reporter: null
        },
        viewport: {
          width: null,
          height: null
        }
      }
    }
  }
}
</script>
