# Typescript 핸드북 정리하기
> https://typescript-kr.github.io/

## keyof

```tsx
interface Car {
    manufacturer: string;
    model: string;
    year: number;
}

type C = keyof Car // "manufacturer" | "model" | "year"
```

## typeof

```tsx
let s = "hello";
let n: typeof s; // string
```

```tsx
type Predicate = (x: unknown) => boolean;
type K = ReturnType<Predicate>;
```

```tsx
function f() {
	return { x: 10, y: 3 };
}
type P = ReturnType<typeof f>;
```

## 교차 타입 vs 유니온 타입

교차 타입과 유니온 타입은 둘 이상의 타입을 합쳐놓은 것과 같지만, 유니온 타입은 `OR` 조건에 해당하고 교차 타입은 `AND` 조건에 해당합니다.

### 유니온 타입

```tsx
type h1 = { a: string; b: string; }
type h2 = { c: number; }
type h3 = h1 | h2;

const hello: h3 = { a: '1', b: '2' }; // ok
const world: h3 = { a: '0' } // ok
```

### 교차 타입

```tsx
type h1 = { a: string; b: string; }
type h2 = { c: number; }
type h3 = h1 & h2;

const hello: h3 = { a: '1', b: '2' }; // typeError
const world: h3 = { a: '1', b: '2', c: 3 } // ok
```

- 모든 조건을 만족해야 함

## 유틸리티 타입

### Pick

```tsx
interface Car {
    manufacturer: string;
    model: string;
    year: number;
}

type B = Pick<Car,'model'> // type { model: string; }
type C = Car['model']; // string
```

- `Pick<T, K>` 는 T에서 프로퍼티 K의 집합을 선택해 타입을 구성한다.