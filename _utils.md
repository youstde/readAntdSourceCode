## _utils

### type

#### tuple

> 接收string，并返回string[]类型数组（元组）

元祖是TS特有的类型，工作机制类似于数组

```tsx
export const tuple = <T extends string[]>(...args:T) => args;
// Button
const ButtonTypes = tuple('default', 'primary', 'ghost', 'dashed', 'link', 'text');
export type ButtonType = typeof ButtonTypes[number];
// ButtonType = 'default' | 'primary' | 'ghost' | 'dashed' | 'link' | 'text'
// 或者可以直接写
export type ButtonType = 'default' | 'primary' | 'ghost' | 'dashed' | 'link' | 'text'

```

```tsx
const ButtonTypes:string[] = ['default', 'primary', 'ghost', 'dashed', 'link', 'text'];

ButtonTypes.push('aaaa') // ts代码检查是通过的，因为ButtonTypes的类型是string[]
```

这种写法我是可以通过push推入任何string类型的值，并且ts代码检查是通过的。

但是如果我想让整个元祖固定成只能是我定义特定值，其他任何虽然满足string类型的值都不能加入到这个元祖中呢

```tsx
const ButtonTypes:['default', 'primary', 'ghost', 'dashed', 'link', 'text'] = ['default', 'primary', 'ghost', 'dashed', 'link', 'text'];

ButtonTypes.push('test') // 这个地方会提示我push的值不满足校验，因为ButtonTypes的类型是特定值的元祖
```

这个时候再看这段代码：

```tsx
export const tuple = <T extends string[]>(...args:T) => args;
```

定义一个泛型的元祖继承于`string[]`,这个时候args的类型并不是string[],而是特定数值的元祖，值为传入的值，比如下面这样👇

```tsx
const ButtonTypes = tuple('default', 'primary', 'ghost')
// ButtonTypes的类型就是['default', 'primary', 'ghost'],而不是string[]
```

