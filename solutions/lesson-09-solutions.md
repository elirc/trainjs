# Lesson 09 Solutions

## Lab 09A

```ts
type User = {
  id: number;
  name: string;
  email: string;
  isAdmin: boolean;
};
```

## Lab 09B

```ts
type Product = {
  id: number;
  name: string;
  inStock: boolean;
};

function getInStockProducts(products: Product[]): Product[] {
  return products.filter(product => product.inStock);
}
```

## Lab 09C

TypeScript helps with API data because it makes expected object shapes explicit. It helps with refactors because renamed fields and broken contracts can be surfaced before runtime.
