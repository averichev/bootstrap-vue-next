# Offcanvas

> Build hidden sidebars into your project. Sidebars can aid in enhancing user interaction or preventing further interaction

<ClientOnly>
  <b-card>
    <b-button @click="click">Show OffCanvas</b-button>
    <b-offcanvas v-model="show" />
  </b-card>
</ClientOnly>

```html
<b-button @click="click">Show OffCanvas</b-button>
<b-offcanvas v-model="show"></b-offcanvas>

<script lang = 'ts'setup>
  import {
    ref,
  } from 'vue'

  const show = ref(false)

  const click = () => {
    show.value = !show.value
  }

</script>
```

## Customizing Location

Customize location with four standard options `top, bottom, start, end`

<ClientOnly>
  <b-card>
    <b-button @click="clickTwo('start')" class="m-2">Show start</b-button>
    <b-button @click="clickTwo('end')" class="m-2">Show end</b-button>
    <b-button @click="clickTwo('bottom')" class="m-2">Show bottom</b-button>
    <b-button @click="clickTwo('top')" class="m-2">Show top</b-button>
    <b-offcanvas v-model="show2" :placement="placement" />
  </b-card>
</ClientOnly>

```html
<b-button @click="click" class="m-2">Show start</b-button>
<b-button @click="click" class="m-2">Show end</b-button>
<b-button @click="click" class="m-2">Show bottom</b-button>
<b-button @click="click" class="m-2">Show top</b-button>
<b-offcanvas v-model="show" :placement="placement" />

<script lang='ts' setup>
  import {ref, computed} from 'vue'

  const show = ref(false)
  const placement = ref('start')

  const click = (place ="start") => {
    placement.value = place
    show.value = !show.value
  }

</script>

```
## Header
The Header by default is always displayed. You can customized the title by using the 
`title` prop or additionally use the `title` slot.

### Hiding the Default Header
Passing in the `no-header` will hide the header.  The header is optionally scoped with the following
noHeader, placement and hide function.

<ClientOnly>
  <b-card>
    <b-button @click="clickThree" class="m-2">Show OffCanvas</b-button>
    <b-offcanvas v-model="show3">
      <div class="p-3">
        <h4 id="sidebar-no-header-title">Custom header sidebar</h4>
        <p>
          Cras mattis consectetur purus sit amet fermentum. Cras justo odio, dapibus ac facilisis
          in, egestas eget quam. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.
        </p>
        <nav class="mb-3">
          <b-nav vertical>
            <b-nav-item active>Active</b-nav-item>
            <b-nav-item href="#link-1">Link</b-nav-item>
            <b-nav-item href="#link-2">Another Link</b-nav-item>
          </b-nav>
        </nav>
      </div>
    </b-offcanvas>
  </b-card>
</ClientOnly>



```html
<b-button @click="click">Show OffCanvas</b-button>
<b-offcanvas id="sidebar-no-header" v-model="show" no-header>
    <div class="p-3">
      <h4 id="sidebar-no-header-title">Custom header sidebar</h4>
      <p>
        Cras mattis consectetur purus sit amet fermentum. Cras justo odio, dapibus ac facilisis
        in, egestas eget quam. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.
      </p>
      <nav class="mb-3">
        <b-nav vertical>
          <b-nav-item active>Active</b-nav-item>
          <b-nav-item href="#link-1">Link</b-nav-item>
          <b-nav-item href="#link-2">Another Link</b-nav-item>
        </b-nav>
      </nav>
    </div>
</b-offcanvas>
```
## Footer
A Footer slot is also available for adding custom content at the bottom of the component.
The slot is optionally scoped including the `hide()` to add closing behavior

<ClientOnly>
<b-card>
    <b-button @click="clickFour" class="m-2">Show OffCanvas with footer</b-button>
</b-card>
 <b-offcanvas id="sidebar-no-header" v-model="show4" no-header>
       <template #footer="{hide}">
          <div class="d-flex justify-content-start bg-dark text-light px-3 py-2">
            <strong class="flex-grow-1">Footer</strong>
            <b-button class="align-self-end" size="sm" @click="hide()">Close</b-button>
          </div>
        </template>
      <div class="p-3">
        <h4 id="sidebar-no-header-title">Custom header sidebar</h4>
        <p>
          Cras mattis consectetur purus sit amet fermentum. Cras justo odio, dapibus ac facilisis
          in, egestas eget quam. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.
        </p>
        <nav class="mb-3">
          <b-nav vertical>
            <b-nav-item active>Active</b-nav-item>
            <b-nav-item href="#link-1">Link</b-nav-item>
            <b-nav-item href="#link-2">Another Link</b-nav-item>
          </b-nav>
        </nav>
      </div>
  </b-offcanvas>
</ClientOnly>


```html
<b-offcanvas id="sidebar-no-header" v-model="show" no-header>
  <template #footer="{hide}">
    <div class="d-flex justify-content-start bg-dark text-light px-3 py-2">
      <strong class="flex-grow-1">Footer</strong>
      <b-button class="align-self-end" size="sm" @click="hide()">Close</b-button>
    </div>
  </template>
  <div class="px-3 py-2">
    <p>
      Cras mattis consectetur purus sit amet fermentum. Cras justo odio, dapibus ac facilisis
      in, egestas eget quam. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.
    </p>
    <b-img src="https://picsum.photos/500/500/?image=54" fluid thumbnail />
  </div>
</b-offcanvas>
```

# Prevent Close
You can prevent closing of the canvas by listening to the `hide` event.
Note if you are customizing and adding your own hide functionality via slots
or other means, you must pass in a trigger. By default the offcanvas will 
pass in triggers for default closing functionality.

<ClientOnly>
    <b-card>
        <b-button @click="clickFive" class="m-2">Show OffCanvas</b-button>
    </b-card>
    <b-offcanvas id="sidebar-no-header" v-model="show5" @hide="validate">
        <div class="px-3 py-2">
          <b-form-input v-model="text" :state="formState" placeholder="Enter your name" />
          <b-form-invalid-feedback id="input-live-feedback">
            Enter at least 3 letters before closing
          </b-form-invalid-feedback>
        </div>
      </b-offcanvas>
</ClientOnly>


```html
<b-offcanvas id="sidebar-no-header" v-model="show" @hide="validate">
  <div class="px-3 py-2">
    <b-form-input v-model="text" :state="formState" placeholder="Enter your name" />
    <b-form-invalid-feedback id="input-live-feedback">
      Enter at least 3 letters before closing
    </b-form-invalid-feedback>
  </div>
</b-offcanvas>
<script setup lang="ts">

import {computed, ref, toRef, useSlots, watch} from 'vue'
import {BvEvent} from './utils'

const show = ref(true)
const text = ref('')
const formState = computed(() => (text.value?.length > 2 ? true : false))

const validate = (event: BvEvent) => {
  if (!formState.value){
    event.preventDefault()
  }
}

</script>
```

# Disabling Back Drop , Focus and Closing
There are several props for disabling default closing behavior.
Prevent closing on back drop with the `noCloseOnBackdrop`. Prevent
closing on  escape with `noCloseOnEsc`. Backdrop can be disabled
by specifying `backdrop` to false.

By default the Back Drop will be focused upon entered. If you wish to remove
this default behavior specify `noFocus` to false


<ClientOnly>
  <ComponentReference></ComponentReference>
</ClientOnly>

<script lang='ts' setup>
  import {ref, computed} from 'vue'

  const show = ref(false)
  const show2 = ref(false)
  const show3 = ref(false)
  const show4 = ref(false)

  const placement = ref('start')

  const click = () => {
    show.value = !show.value
  }

   const clickTwo = (place ="start") => {
    placement.value = place
    show2.value = !show2.value
  }

  const clickThree= () =>{
    show3.value = !show3.value
  }

  const clickFour= () =>{
    show4.value = !show4.value
  }

  const clickFive= () =>{
    show5.value = !show5.value
  }


const text = ref('')
const formState = computed(() => (text.value?.length > 2 ? true : false))

  const validate = (event: BvEvent) => {
  if (!formState.value){
    event.preventDefault()
  }
}

</script>
