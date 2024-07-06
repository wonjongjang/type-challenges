# Question

For given a tuple, you need create a generic `Length`, pick the length of the tuple

```ts
type tesla = ['tesla', 'model 3', 'model X', 'model Y']
type spaceX = ['FALCON 9', 'FALCON HEAVY', 'DRAGON', 'STARSHIP', 'HUMAN SPACEFLIGHT']

type teslaLength = Length<tesla>  // expected 4
type spaceXLength = Length<spaceX> // expected 5
```

# Answer

```ts
/* _____________ Your Code Here _____________ */

type Length<T extends readonly string[]> = T['length']
```

```ts
/* _____________ Test Cases _____________ */

import type { Equal, Expect } from '@type-challenges/utils'

const tesla = ['tesla', 'model 3', 'model X', 'model Y'] as const
const spaceX = ['FALCON 9', 'FALCON HEAVY', 'DRAGON', 'STARSHIP', 'HUMAN SPACEFLIGHT'] as const

type cases = [
  Expect<Equal<Length<typeof tesla>, 4>>,
  Expect<Equal<Length<typeof spaceX>, 5>>,
  // @ts-expect-error
  Length<5>,
  // @ts-expect-error
  Length<'hello world'>,
]
```

# Reference

- [readonly and const](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#readonly-and-const)
