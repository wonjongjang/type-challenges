# Question

Implement the type version of `Array.unshift`

For example:

```ts
type Result = Unshift<[1, 2], 0>; // [0, 1, 2]
```

# Answer

```ts
/* _____________ Your Code Here _____________ */

type Unshift<T extends unknown[], U> = [U, ...T];
```

```ts
/* _____________ Test Cases _____________ */

import type { Equal, Expect } from '@type-challenges/utils';

type cases = [Expect<Equal<Unshift<[], 1>, [1]>>, Expect<Equal<Unshift<[1, 2], 0>, [0, 1, 2]>>, Expect<Equal<Unshift<['1', 2, '3'], boolean>, [boolean, '1', 2, '3']>>];
```
