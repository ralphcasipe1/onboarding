### Tech
- KoaJS
- Typescript
- Mongoose

- Graphql (Apollo Server)


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