<template>
  <c-box
    boxShadow=" 0 4px 6px 0 rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)"
    p="10"
  >
    <form @submit.prevent>
      <c-simple-grid :columns="[1, null, 2]" spacing-x="40px">
        <CFormControl py="2" isRequired>
          <c-form-label for="pages">Pages</c-form-label>
          <c-textarea placeholder="Pages" id="pages" v-model="form.pages" />
          <c-form-helper-text
            >Please divide pages with comma and space
          </c-form-helper-text>
        </CFormControl>
        <c-box>
          <CFormControl py="2">
            <c-form-label for="title">Title</c-form-label>
            <c-input placeholder="Title" id="title" v-model="form.title" />
          </CFormControl>
          <CFormControl py="2">
            <c-form-label for="fileName">Filename</c-form-label>
            <c-input
              placeholder="Filename"
              id="fileName"
              v-model="form.fileName"
            />
          </CFormControl>
          <CFormControl py="2">
            <c-form-label for="resultsDir">Results dir</c-form-label>
            <c-input
              placeholder="Title"
              id="resultsDir"
              v-model="form.resultsDir"
            />
          </CFormControl>
        </c-box>
      </c-simple-grid>

      <CHeading as="h2" size="sm" pt="4">
        Axe config
      </CHeading>
      <CDivider />
      <c-simple-grid :columns="[1, null, 2]" spacing-x="40px">
        <CFormControl py="2">
          <c-form-label for="reporter">Reporter</c-form-label>
          <c-input
            placeholder="Reporter"
            id="reporter"
            v-model="form.axeConfig.reporter"
          />
        </CFormControl>
      </c-simple-grid>

      <CHeading as="h2" size="sm" pt="4">
        Viewport
      </CHeading>
      <CDivider />
      <c-simple-grid :columns="[1, null, 2]" spacing-x="40px">
        <CFormControl py="2">
          <c-form-label for="width">Width (px)</c-form-label>
          <c-input
            type="number"
            placeholder="Width"
            id="width"
            v-model="form.viewport.width"
          />
        </CFormControl>
        <CFormControl py="2">
          <c-form-label for="height">Height (px)</c-form-label>
          <c-input
            type="number"
            placeholder="Height"
            id="height"
            v-model="form.viewport.height"
          />
        </CFormControl>
      </c-simple-grid>

      <CHeading as="h2" size="sm" pt="4">
        Basic auth configuration
      </CHeading>
      <CDivider />
      <c-simple-grid :columns="[1, null, 2]" spacing-x="40px">
        <CFormControl py="2">
          <c-form-label for="username">Username</c-form-label>
          <c-input
            placeholder="Username"
            id="username"
            v-model="form.basicAuth.username"
          />
        </CFormControl>
        <CFormControl py="2">
          <c-form-label for="password">Password</c-form-label>
          <c-input
            type="password"
            placeholder="Password"
            id="password"
            v-model="form.basicAuth.password"
          />
        </CFormControl>
      </c-simple-grid>

      <c-simple-grid :columns="[1, null, 2]" spacing-x="40px">
        <CButton
          @click="onSubmit"
          mt="2"
          variant-color="blue"
          :disabled="disabled"
        >
          Send
        </CButton>
      </c-simple-grid>
    </form>
  </c-box>
</template>

<script>
import {
  CBox,
  CFormControl,
  CFormLabel,
  CInput,
  CTextarea,
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
    CTextarea,
    CInput,
    CDivider,
    CHeading,
    CButton,
    CSimpleGrid
  },

  data() {
    return {
      form: {
        pages: null,
        title: null,
        fileName: null,
        resultsDir: null,
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
    };
  },

  computed: {
    disabled() {
      return (
        !this.form.pages
      );
    }
  },

  methods: {
    onSubmit() {
      const form = this.form
      const data = {
        ...form,
        pages: form.pages.split(', '),
        title: form.title || undefined,
        fileName: form.fileName || undefined,
        resultsDir: form.resultsDir || undefined,
        basicAuth:
          form.basicAuth.username && form.basicAuth.password
            ? form.basicAuth : undefined,
        axeConfig: form.axeConfig.reporter ? form.axeConfig : undefined,
        viewport:
          form.viewport.width && form.viewport.height
            ? form.viewport
            : undefined
      }
      this.$emit('submit', data)
      this.clear()
    },

    clear() {
      this.form = {
        pages: null,
        title: null,
        fileName: null,
        resultsDir: null,
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
