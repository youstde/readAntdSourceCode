## _utils

### type

#### tuple

> 接收参数并返回数组

为什么要写一个方法去处理这个场景呢，直接写的时候就写成一个数组不香吗？重点在这里：

```tsx
export const tuple = <T extends string[]>(...args:T) => args;

// 使用场景
const ButtonTypes = tuple('default', 'primary', 'ghost', 'link');
export type ButtonTypes = typeof ButtonTypes[number];
// ButtonTypes => 'default' | 'primary' | 'ghost' | 'link'

// 如
```

