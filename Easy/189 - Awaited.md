# Question

If we have a type which is a wrapped type like Promise, how we can get the type which is inside the wrapped type?

For example: if we have `Promise<ExampleType>` how to get ExampleType?

```ts
type ExampleType = Promise<string>

type Result = MyAwaited<ExampleType> // string
```

# Answer

```ts
/* _____________ Your Code Here _____________ */

type MyAwaited<T> = T extends null | undefined
  ? T
  : T extends object & {
      then(onfulfilled: infer F, ...args: infer _): any;
    }
    ? F extends (value: infer V, ...args: infer _) => any
      ? MyAwaited<V>
      : never
    : T;
```

```ts
/* _____________ Test Cases _____________ */

import type { Equal, Expect } from '@type-challenges/utils'

type X = Promise<string>
type Y = Promise<{ field: number }>
type Z = Promise<Promise<string | number>>
type Z1 = Promise<Promise<Promise<string | boolean>>>
type T = { then: (onfulfilled: (arg: number) => any) => any }

type cases = [
  Expect<Equal<MyAwaited<X>, string>>,
  Expect<Equal<MyAwaited<Y>, { field: number }>>,
  Expect<Equal<MyAwaited<Z>, string | number>>,
  Expect<Equal<MyAwaited<Z1>, string | boolean>>,
  Expect<Equal<MyAwaited<T>, number>>,
]
```

# Reference

- [Awaited<Type>](https://www.typescriptlang.org/docs/handbook/utility-types.html#awaitedtype)
