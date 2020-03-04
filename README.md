# vue-greeklish-search

## Installation
Use the package manager [npm](https://www.npmjs.com/) to install vue-greeklish-search.
```bash
npm install --save vue-greeklish-search
```

## Usage

```vue
import GreeklishSearch from 'vue-greeklish-search';

Vue.use(GreeklishSearch);
```

## Usage Component

```vue
<GreeklishSearch v-model="text"/>

export default {
  data() {
    return {
      text: null
    }
  },
}
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
