# Bedrock Vue Component

# Installation

### Use Locally

```
npm i -D ../bedrock-core-vue
```

### Use Npm version

```
npm i -D yormy-bedrock-core-vue
```

# Using components

```
import { HelloComponent } from "bedrock-vu--component";

components: {
    HelloComponent
}
  
```

# Building & Publishing

## step 1 build the package

```
npm install
npm run build
```

## step 2: Publish

### setup for npm

``` 
npm adduser
```

### publish

```
npm publish
```

# Typescript

``` 
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { SampleComponent } from "vue-component-library";

@Component({
  components: {
    SampleComponent
  }
})
export default class App extends Vue {}
</script>
```
