# Vue 3 + Typescript + Vite

This template should help get you started developing with Vue 3 and Typescript in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur). Make sure to enable `vetur.experimental.templateInterpolationService` in settings!

### If Using `<script setup>`

[`<script setup>`](https://github.com/vuejs/rfcs/pull/227) is a feature that is currently in RFC stage. To get proper IDE support for the syntax, use [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar) instead of Vetur (and disable Vetur).

## Type Support For `.vue` Imports in TS

Since TypeScript cannot handle type information for `.vue` imports, they are shimmed to be a generic Vue component type by default. In most cases this is fine if you don't really care about component prop types outside of templates. However, if you wish to get actual prop types in `.vue` imports (for example to get props validation when using manual `h(...)` calls), you can use the following:

### If Using Volar

Run `Volar: Switch TS Plugin on/off` from VSCode command palette.

### If Using Vetur

1. Install and add `@vuedx/typescript-plugin-vue` to the [plugins section](https://www.typescriptlang.org/tsconfig#plugins) in `tsconfig.json`
2. Delete `src/shims-vue.d.ts` as it is no longer needed to provide module info to Typescript
3. Open `src/main.ts` in VSCode
4. Open the VSCode command palette
5. Search and run "Select TypeScript version" -> "Use workspace version"

### Command per-setup to force run ✔

- `npm install --save-dev @types/node` for fix some types
- `npm install vite-plugin-components` for auto-add global component (config in file vite)
- 





### New features of vite uses ✔

- Please take a look closely to file `vite.config.js`, its contain some feature options good.
```
// Declare the path "@" instead of "/src"
alias: [{find: "@", replacement: path.resolve(__dirname, '/src')}
// Declare the path of variable source to use variable in style tag in components
css: {
  preprocessorOptions: {
    scss: {
      additionalData: `@import "./src/assets/stylesheets/_variables";` 
    } 
  } 
},
// 
```

### Step ✔
- Sử dụng attribute `lang` tại `<script>` 

```
<script lang="ts">
...
</script>
```

- Function `defineComponent` tại export được gọi tới để kiểm tra `out-of-the-box type checking` cho component

```
import { defineComponent } from 'vue'
export default defineComponent({
  ...
})
```

- Cùng xem lại các kiểu dữ liệu trong `typeScript`:

| All    | Loại                                                                                              |
| -------| :-------------------------------------------------------------------------------------------------|
| Tất cả | boolean , number , string , array , object , tuple , enum , any , void , undefined , null , never |
| Common | boolean , number , string , array , object, void , undefined , null                               |

- Cú pháp `PropType` để có thể sử dụng được các kiểu generic type (thay vì kiểu prop type system đơn thuần như vue2)
- Here we’re still using Vue’s default prop type system (the Object part), but we’re only using it as a middleman. <br> We first set the prop type as Object, but we soon converted it to CharCountParams through PropType.<br> (PropType is a TypeScript type intended for this situation.)

```
// Props type system Vue2
export default {
  props: {
    params: {
      type: Object,
      required: true,
    }
  },
}
```

```
// Prop type new in Vue3
import { PropType , defineComponent } from 'vue'
import { CharCountParams } from "@/@types/CharCountParams.interface"

export default defineComponent({
  props: {
    params: {
      type: Object as PropType<CharCountParams>,
      required: true,
    }
  },
})
```

- 



