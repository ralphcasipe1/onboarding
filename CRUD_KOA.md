### CRUD VENDOR
- KoaJS
- Typescript
- Mongoose

Write a function that can **CRUD** a `vendor` in **RESTful API**.

The vendor object shape

```typescript
enum VendorType {
  Seamless = 'SEAMLESS'
  Transfer = 'TRASNFER'
};

type Vendor = {
  _id: string;
  name: string;
  type: VendorType;
  dateTimeCreated: Date;
  dateTimeUpdated: Date; 
}
```

### GraphQL
- [KoaJS](https://github.com/koajs/koa)
  - `npm i -S koa`
  - `npm i -D @types/koa`

- [TypeScript](https://www.typescriptlang.org/)
  - `npm i -D typescript`

- [Mongoose](https://github.com/Automattic/mongoose)
  - `npm i -S mongoose`
  - `npm i -D @types/mongoose`