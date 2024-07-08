# Question

Implement the built-in `Exclude<T, U>`

>  Exclude from `T` those types that are assignable to `U`

```ts
type Result = MyExclude<'a' | 'b' | 'c', 'a'> // 'b' | 'c'
```

# Answer

```ts
/* _____________ Your Code Here _____________ */

type MyExclude<T, U> = T extends U ? never : T
```

```ts
/* _____________ Test Cases _____________ */

import type { Equal, Expect } from '@type-challenges/utils'

type cases = [
  Expect<Equal<MyExclude<'a' | 'b' | 'c', 'a'>, 'b' | 'c'>>,
  Expect<Equal<MyExclude<'a' | 'b' | 'c', 'a' | 'b'>, 'c'>>,
  Expect<Equal<MyExclude<string | number | (() => void), Function>, string | number>>,
]
```

# Reference

- [Exclude<UnionType, ExcludedMembers>](https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers)
- [Distributive Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#distributive-conditional-types)
