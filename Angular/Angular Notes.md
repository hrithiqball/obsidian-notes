## 1. Services for temporal data storage and sharing

Services are really supportive, not only to send requests to the backend but also to temporally save data that is used in multiple components. Below you can find an example of an e-commerce shopping cart implementation extracted from the Angular Documentation.

However, this implementation is a handy trick to avoid the case of creating long `@Input()` chains across many components to pass always the same data.

Just need to add the service in the constructor of the components that need this storage system to use it. Even when navigating through the rest of the platform, the information will persist.

```ts
@Injectable({
	providedIn: "root",
})
export class CartService {
	items: Product[] = [];

	addToCart(product: Product) {
		this.items.push(product);
	}

	getItems() {
		return this.items;
	}

	clearCart() {
		this.items = [];
		return this.items;
	}
}
```

## 2. NgStyle

`[NgStyle]` is an HTML attribute directive that updates styles for the containing HTML element. Sets one or more style properties, specified as colon-separated key-value pairs, just like CSS.

I found this Angular directive particularly useful to display dynamic images and at the same time compose complex layouts with multiple nested backgrounds and images.

This way, you can manage objects in typescript that gather not only text attributes but also multimedia attributes, so you can retrieve all data in running time and display it in an organized way. See the example below.

```html
<div class="row">
	<div class="col-md-6" *ngFor="let team of teams; index as i">
		<div
			class="team-card d-flex justify-content-center "
			[ngStyle]="{'background-image': 'url(' + team.bgPicture + ')'}"
		>
			<div
				class="row players-bg d-flex justify-content-center center-vertical"
				[ngStyle]="{'background-image': 'url(' + team.playersPicture + ')'}"
			>
				<div class="row d-flex justify-content-center">
					<label class="team-name" style="text-align: center">
						{{ team.name | uppercase }}
					</label>
				</div>
			</div>
		</div>
	</div>
</div>
```

## 3. Type Aliases

TypeScript allows you to create custom types using a feature called **type aliases**. The main difference between features `type` alias and `interface` is that type alias creates a new name for the type, whereas`interface` creates a new name for the shape of the object.

For example, you can use a **type alias** to create a custom type for a point in a two-dimensional space:

```ts
type Point = { x: number, y: number };
let point: Point = { x: 0, y: 0 };

Type aliases can also be used to create complex types, such as a **union type** or an **intersection type**.

type User = { name: string, age: number };
type Admin = { name: string, age: number, privileges: string[] };
type SuperUser = User & Admin;
```

## 4. Using the `unknown` Type

The unknown type is a powerful and restrictive type that was introduced in TypeScript 3.0. It is a more restrictive type than `any` and it can help you to prevent unintended type errors.

Unlike `any`, when you use the unknown type, TypeScript will not allow you to perform any operation on a value unless you first check its type. This can help you to catch type errors at compile-time, instead of at runtime.

For example, you can use the unknown type to create a more type-safe function:

```ts
function printValue(value: unknown) {
	if (typeof value === "string") {
		console.log(value);
	} else {
		console.log("Not a string");
	}
}
```

You can also use the unknown type to create more type-safe variables:

```ts
let value: unknown = "hello";
let str: string = value; // Error: Type 'unknown' is not assignable to type 'string'.
```

## 5. “never”

In TypeScript, `never` is a special type that represents values that will never occur. It’s used to indicate that a function will not return normally, but will instead throw an error. This is a great way to indicate to other developers (and the compiler) that a function can’t be used in certain ways, this can help to catch potential bugs.

For example, consider the following function that throws an error if the input is less than 0:

```ts
function divide(numerator: number, denominator: number): number {
	if (denominator === 0) {
		throw new Error("Cannot divide by zero");
	}
	return numerator / denominator;
}
```

Here, the function `divide` is declared to return a number, but if the denominator is zero, it will throw an error. To indicate that this function will not return normally in this case, you can use **never** as the return type:

```ts
function divide(numerator: number, denominator: number): number | never {
	if (denominator === 0) {
		throw new Error("Cannot divide by zero");
	}
	return numerator / denominator;
}
```

## 6. Using the `keyof` operator

The `keyof` operator is a powerful feature of TypeScript that allows you to create a type that represents the keys of an object. It can be used to make it clear which properties are allowed for an object.

For example, you can use the `keyof` operator to create a more readable and maintainable type for an object:

```ts
interface User {
	name: string;
	age: number;
}

type UserKeys = keyof User; // "name" | "age"
```

You can also use the `keyof` operator to create more type-safe functions that take an object and a key as arguments:

```ts
function getValue<T, K extends keyof T>(obj: T, key: K) {
	return obj[key];
}
let user: User = { name: "John", age: 30 };
console.log(getValue(user, "name")); // "John"
console.log(getValue(user, "gender")); // Error: Argument of type '"gender"' is not assignable to parameter of type '"name" | "age"'.
```

## 7. Using Enums

Enums, short for enumerations, are a way to define a set of named constants in TypeScript. They can be used to create a more readable and maintainable code, by giving a meaningful name to a set of related values.

For example, you can use an enum to define a set of possible status values for an order:

```ts
enum OrderStatus {
	Pending,
	Processing,
	Shipped,
	Delivered,
	Cancelled,
}

let orderStatus: OrderStatus = OrderStatus.Pending;
```

Enums can also have a custom set of numeric values or strings.

```ts
enum OrderStatus {
	Pending = 1,
	Processing = 2,
	Shipped = 3,
	Delivered = 4,
	Cancelled = 5,
}

let orderStatus: OrderStatus = OrderStatus.Pending;
```

Always name an enum with the first capital letter and the name has to be in singular form, as a part of the naming convention.

## 8. Using Namespaces

Namespaces are a way to organize your code and prevent naming collisions. They allow you to create a container for your code, where you can define variables, classes, functions, and interfaces.

For example, you can use a namespace to group all the code related to a specific feature:

```ts
namespace OrderModule {
	export class Order {
		/* … */
	}
	export function cancelOrder(order: Order) {
		/* … */
	}
	export function processOrder(order: Order) {
		/* … */
	}
}
let order = new OrderModule.Order();
OrderModule.cancelOrder(order);
```

You can also use namespaces to prevent naming collisions by providing a unique name for your code:

```ts
namespace MyCompany.MyModule {
	export class MyClass {
		/* … */
	}
}

let myClass = new MyCompany.MyModule.MyClass();
```

It’s important to note that namespaces are similar to modules, but they are used to organize the code and prevent naming collisions, while modules are used to load and execute the code.

## 9. Using Utility Types

Utility types are a built-in feature of TypeScript that provide a set of predefined types to help you write better type-safe code. They allow you to perform common type operations and manipulate types in a more convenient way.

For example, you can use the `Pick` utility type to extract a subset of properties from an object type:

```ts
type User = { name: string; age: number; email: string };
type UserInfo = Pick<User, "name" | "email">;
```

You can also use the `Exclude` utility type to remove properties from an object type:

```ts
type User = { name: string; age: number; email: string };
type UserWithoutAge = Exclude<User, "age">;
```

You can use the `Partial` utility type to make all properties of a type optional:

```ts
type User = { name: string; age: number; email: string };
type PartialUser = Partial<User>;
```
