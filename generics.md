Generics in typescript

// Array
// last
// makeArr: 2 generics, return, overwrite inference, default value
// addFullName: extends
// interfaces
// props
// useState
// jsx generic

```
// Allows us to pass anytime but still checks to 
// see if its consistant
const last = <T>(arr: T[]): T => {
  return arr[arr.length - 1];
};

// works for both examples
const l = last([1, 2, 3]);

const l2 = last<string>(["a", "b", "c"]);

const makeArr = <X, Y>(x: X, y: Y): [X, Y] => {
  return [x, y];
};

const v = makeArr(5, 6);
const v2 = makeArr("a", "b");
const v3 = makeArr<string | null, number>("a", 5);

const makeFullName = <T extends { firstName: string; lastName: string }>(
  obj: T
) => {
  return {
    ...obj,
    fullName: obj.firstName + " " + obj.lastName
  };
};

// this will work since it only has first and last to be required
const v4 = makeFullName({ firstName: "bob", lastName: "junior", age: 15 });
// this will not work since firstName is required
// const v5 = makeFullName({ another: "bob", lastName: "junior", age: 15 });

interface Tab<T> {
  id: string;
  position: number;
  data: T;
}

type NumberTab = Tab<number>;

```

