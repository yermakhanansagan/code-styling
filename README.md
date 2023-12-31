
# ADATA Code Style Guide for FrontEnd

Стилизация кода для Фронтенд разработчиков (js, ts, vue)





## Ознокомится тем для чего это нужно можно здесь

[Тык](https://habr.com/ru/companies/manychat/articles/468953/)

Коротко говоря мне захотелось подушнить

### Naming

* Название файлов

Обычные файлы Vue и папки называем в kebab-case прим. my-button.vue, single-select
Helper функции называем в camelCase.ts

* Давать понятные названия переменным.

```javasript
// плохо

const a

// хорошо

const user
```

* Давать глагольные названия функциям (также можно добавлять префиксы действий get-/set-/map-/merge-).

```javasript
// Плохо: 
const filteredUsers = (users) => users.filter(...) // это переменная или функция?

// Хорошо: 
const filterUsers = (users) => users.filter(...)
```
* Типы и классы должны начинаться с большой буквы. Добавление префикса T/I в начале типа в JavaScript, по мне, излишне.

```javascript
// Плохо:
type user = {id: string};
type TUser = {id: string};
interface IMovie = {id: string};

// Хорошо:
type User = {id: string};
```

## JavaScript
- Language features

### Functions

В JavaScript есть два типа объявления функции Function Declaration и Function Expression.

#### Function Declaration

Использовать в большх блоках кода где функция будет иметь внутри несколь действий либо блоков прим.

```javascript
async function submit() {
  v$.value.$touch()
  if (!v$.value.$invalid) {
    const { data, error } = await request()
    if (data) {
      useCookie('tokenTime', { maxAge: data.expires_in }).value = data.expires_in
      accessToken.value = data.access_token
      refreshCookie.value = data.refresh_token
      $toast.success(t('toast.success'))
      setTimeout(() => {
        router.push('/main/personal-area')
      }, 1000)
    }
  } else {
    // invalid
  }
}
```

#### Function Expression

Может работать без return не надо использовать return, использовать в случаях когда код имеет функционал на одну строку прим.

```javascript
// Плохо:
const getUsers = (users) => {
  return users.value = data
}

// Хорошо:
const getUsers = (data) => (users.value = data)
```
## TypeScript

- Typing

### Typing primitives

Не нужно типизировать примитивные типы данных, Typescript сам это сделает.

```typescript
// Плохо:

const isLoading = ref<boolean>(true)
const num = ref<number>(0)
const str = ref<string>('')

// Хорошо:

const isLoading = ref(true)
const num = ref(0)
const str = ref('')
```

### Any

Не использовать any, unknown типизировать все (в редких случаях семантики можно использовать unknown).
[Почитайте тут](https://www.typescriptlang.org/docs/handbook/utility-types.html) для большего флекса

### Interface vs Type

Использовать во многих случаях Type так как многие функции Type трудно или невозможно реализовать с помощью Interface. Например, TypeScript предоставляет богатые функции, такие как условные типы, универсальные типы, защита типов, расширенные типы и многое другое. Вы можете использовать их для создания хорошо ограниченной системы типов, которая сделает ваше приложение строго типизированным. Интерфейс не может этого достичь.
Interface использовать только в случаях реализций их в class


## Vue
- File Structure
- Code Structure

### File Structure
Использовать структуру как в примере снизу для более удобного скролинга между блоками кода
```html
<script setup lang='ts'>

</script>

<template>

</template>

<style scoped>

</style>
```

#### Import managment

Очередность import файлов
- Сторонние модули
- Компоненты которые есть в проекте
- Иконки в случае использования NuxtSVGO
- Composables, helpers
- Types

```javascript
import { useVuelidate } from '@vuelidate/core/dist'
import { helpers, maxLength, minLength, required } from '@vuelidate/validators/dist'

import Foo from '~/components/foo.vue'
import Bar from '~/components/bar.vue'

import SomeIcon from '~/icons/SomeIcon.svg'

import { someComposable } from '~/composables/someComposable'

import type { someType } from '~/types/someType.ts'
```

### Code Structure
- Vue or Nuxt configs
- App global variables and funtions
- defineOptions
- types
- defineProps
- define Emits
- variables
- computed functions
- functions
- watchers
- lifecycle hooks

```javascript
<script setup lang="ts">
const { $api, $toast } = useNuxtApp()

const { t } = useI18n()

defineOptions({
  inheritAttrs: false,
  customOptions: {
    /* ... */
  }
})

type Props = {
  foo: string
  bar?: number
}

type Emits = {
  (e: 'change', id: number): void
  (e: 'update', value: string): void
}

const props = defineProps<Props>()

const emit = defineEmits<Emits>()

const value = someValue
const modelValue = ref()

const foo = () => modelValue.value = 'b';

function bar() {
    if (false) return
    foo()
}


watch(value, () => foo);

onMounted(() => modelValue.value = 'b');
</setup>
```

## Git

Оформление commit

Плохо:
```git
git commit -m "fix"
git commit -m "refactor"
git commit -m "some changes"
```

Хорошо:
```git
git commit -m "branch feat/fix/refactor(file): description"
```



