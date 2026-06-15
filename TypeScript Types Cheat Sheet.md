- [[#1. Basic Types|1. Basic Types]]
	- [[#1. Basic Types#Primitive types|Primitive types]]
	- [[#1. Basic Types#`any`|`any`]]
	- [[#1. Basic Types#`unknown`|`unknown`]]
	- [[#1. Basic Types#`never`|`never`]]
	- [[#1. Basic Types#`void`|`void`]]
- [[#2. Type Annotations and Inference|2. Type Annotations and Inference]]
	- [[#2. Type Annotations and Inference#Type annotations|Type annotations]]
	- [[#2. Type Annotations and Inference#Type inference|Type inference]]
- [[#3. Arrays and Tuples|3. Arrays and Tuples]]
	- [[#3. Arrays and Tuples#Arrays|Arrays]]
	- [[#3. Arrays and Tuples#Tuples|Tuples]]
- [[#4. Object Types|4. Object Types]]
	- [[#4. Object Types#Inline object types|Inline object types]]
	- [[#4. Object Types#Optional properties|Optional properties]]
	- [[#4. Object Types#`readonly` properties|`readonly` properties]]
	- [[#4. Object Types#Index signatures|Index signatures]]
- [[#5. Unions, Intersections, and Literals|5. Unions, Intersections, and Literals]]
	- [[#5. Unions, Intersections, and Literals#Union types|Union types]]
	- [[#5. Unions, Intersections, and Literals#Intersection types|Intersection types]]
	- [[#5. Unions, Intersections, and Literals#Literal types|Literal types]]
- [[#6. Type Aliases and Interfaces|6. Type Aliases and Interfaces]]
	- [[#6. Type Aliases and Interfaces#Type aliases|Type aliases]]
	- [[#6. Type Aliases and Interfaces#Interfaces|Interfaces]]
	- [[#6. Type Aliases and Interfaces#Interface vs. type alias|Interface vs. type alias]]
- [[#7. Function Types|7. Function Types]]
	- [[#7. Function Types#Function declarations|Function declarations]]
	- [[#7. Function Types#Function type expressions|Function type expressions]]
	- [[#7. Function Types#Optional parameters|Optional parameters]]
	- [[#7. Function Types#Default parameters|Default parameters]]
	- [[#7. Function Types#Rest parameters|Rest parameters]]
	- [[#7. Function Types#`this` types in functions|`this` types in functions]]
- [[#8. Generics|8. Generics]]
	- [[#8. Generics#Basic generics|Basic generics]]
	- [[#8. Generics#Generic constraints|Generic constraints]]
	- [[#8. Generics#Generic defaults|Generic defaults]]
	- [[#8. Generics#Generic keys|Generic keys]]
- [[#9. TypeScript Type Operators|9. TypeScript Type Operators]]
	- [[#9. TypeScript Type Operators#`keyof`|`keyof`]]
	- [[#9. TypeScript Type Operators#`typeof`|`typeof`]]
	- [[#9. TypeScript Type Operators#`in`|`in`]]
	- [[#9. TypeScript Type Operators#`as`|`as`]]
	- [[#9. TypeScript Type Operators#`satisfies`|`satisfies`]]
	- [[#9. TypeScript Type Operators#`infer`|`infer`]]
- [[#10. Type Assertions and Const Assertions|10. Type Assertions and Const Assertions]]
	- [[#10. Type Assertions and Const Assertions#Type assertions|Type assertions]]
	- [[#10. Type Assertions and Const Assertions#Const assertions: `as const`|Const assertions: `as const`]]
- [[#11. Type Narrowing and Type Guards|11. Type Narrowing and Type Guards]]
	- [[#11. Type Narrowing and Type Guards#Common narrowing techniques|Common narrowing techniques]]
	- [[#11. Type Narrowing and Type Guards#`typeof` narrowing|`typeof` narrowing]]
	- [[#11. Type Narrowing and Type Guards#`instanceof` narrowing|`instanceof` narrowing]]
	- [[#11. Type Narrowing and Type Guards#Truthiness narrowing|Truthiness narrowing]]
	- [[#11. Type Narrowing and Type Guards#User-defined type guards|User-defined type guards]]
	- [[#11. Type Narrowing and Type Guards#Assertion functions|Assertion functions]]
- [[#12. Discriminated Unions|12. Discriminated Unions]]
- [[#13. Enums|13. Enums]]
	- [[#13. Enums#Numeric enums|Numeric enums]]
	- [[#13. Enums#String enums|String enums]]
	- [[#13. Enums#Enum alternative: union literals|Enum alternative: union literals]]
- [[#14. Utility Types|14. Utility Types]]
	- [[#14. Utility Types#Quick reference|Quick reference]]
	- [[#14. Utility Types#`Partial<T>`|`Partial<T>`]]
	- [[#14. Utility Types#`Required<T>`|`Required<T>`]]
	- [[#14. Utility Types#`Readonly<T>`|`Readonly<T>`]]
	- [[#14. Utility Types#`Pick<T, K>`|`Pick<T, K>`]]
	- [[#14. Utility Types#`Omit<T, K>`|`Omit<T, K>`]]
	- [[#14. Utility Types#`Record<K, V>`|`Record<K, V>`]]
	- [[#14. Utility Types#`Exclude<T, U>`|`Exclude<T, U>`]]
	- [[#14. Utility Types#`Extract<T, U>`|`Extract<T, U>`]]
	- [[#14. Utility Types#`NonNullable<T>`|`NonNullable<T>`]]
	- [[#14. Utility Types#`ReturnType<T>`|`ReturnType<T>`]]
	- [[#14. Utility Types#`Parameters<T>`|`Parameters<T>`]]
	- [[#14. Utility Types#`ConstructorParameters<T>`|`ConstructorParameters<T>`]]
	- [[#14. Utility Types#`InstanceType<T>`|`InstanceType<T>`]]
	- [[#14. Utility Types#`Awaited<T>`|`Awaited<T>`]]
- [[#15. Mapped Types|15. Mapped Types]]
	- [[#15. Mapped Types#Mapping value types|Mapping value types]]
	- [[#15. Mapped Types#Mapping modifiers|Mapping modifiers]]
	- [[#15. Mapped Types#Key remapping with `as`|Key remapping with `as`]]
- [[#16. Conditional Types|16. Conditional Types]]
	- [[#16. Conditional Types#Conditional types distribute over unions|Conditional types distribute over unions]]
	- [[#16. Conditional Types#Real-world example: async result extraction|Real-world example: async result extraction]]
- [[#17. Template Literal Types|17. Template Literal Types]]
- [[#18. Recursive Types|18. Recursive Types]]
- [[#19. Branded Types|19. Branded Types]]
- [[#20. Declaration Merging|20. Declaration Merging]]
	- [[#20. Declaration Merging#Interface merging|Interface merging]]
- [[#21. Module Typing Basics|21. Module Typing Basics]]
	- [[#21. Module Typing Basics#Exporting types|Exporting types]]
	- [[#21. Module Typing Basics#Importing types|Importing types]]
	- [[#21. Module Typing Basics#Typing default and named exports|Typing default and named exports]]
	- [[#21. Module Typing Basics#Ambient module declarations|Ambient module declarations]]
	- [[#21. Module Typing Basics#Global declarations|Global declarations]]
- [[#22. React Typing Basics|22. React Typing Basics]]
	- [[#22. React Typing Basics#Typing props|Typing props]]
	- [[#22. React Typing Basics#Typing children|Typing children]]
	- [[#22. React Typing Basics#Typing event handlers|Typing event handlers]]
	- [[#22. React Typing Basics#Reusing native element props|Reusing native element props]]
	- [[#22. React Typing Basics#Generic components|Generic components]]
- [[#23. Type-Related Compiler Options|23. Type-Related Compiler Options]]
	- [[#23. Type-Related Compiler Options#Recommended strictness options|Recommended strictness options]]
	- [[#23. Type-Related Compiler Options#Module and emit-related options that affect types|Module and emit-related options that affect types]]
- [[#24. Common Mistakes and Best Practices|24. Common Mistakes and Best Practices]]
	- [[#24. Common Mistakes and Best Practices#Prefer `unknown` over `any` for untrusted values|Prefer `unknown` over `any` for untrusted values]]
	- [[#24. Common Mistakes and Best Practices#Do not confuse type assertions with runtime validation|Do not confuse type assertions with runtime validation]]
	- [[#24. Common Mistakes and Best Practices#Be careful with optional properties|Be careful with optional properties]]
	- [[#24. Common Mistakes and Best Practices#Keep unions discriminated|Keep unions discriminated]]
	- [[#24. Common Mistakes and Best Practices#Avoid overly broad object types|Avoid overly broad object types]]
	- [[#24. Common Mistakes and Best Practices#Use `satisfies` for config objects|Use `satisfies` for config objects]]
	- [[#24. Common Mistakes and Best Practices#Prefer union literals over enums for many app states|Prefer union literals over enums for many app states]]
	- [[#24. Common Mistakes and Best Practices#Add return types to exported functions|Add return types to exported functions]]
	- [[#24. Common Mistakes and Best Practices#Use exhaustive checks with `never`|Use exhaustive checks with `never`]]
	- [[#24. Common Mistakes and Best Practices#Keep type-level programming readable|Keep type-level programming readable]]
	- [[#24. Common Mistakes and Best Practices#Model domain concepts, not just data shapes|Model domain concepts, not just data shapes]]
	- [[#24. Common Mistakes and Best Practices#Practical checklist|Practical checklist]]


---
## 1. Basic Types

TypeScript adds static types to JavaScript values. Most basic types correspond directly to JavaScript runtime primitives.

### Primitive types

| Type | Meaning | Example |
|---|---|---|
| `string` | Text | `"active"` |
| `number` | All JS numbers: integers, floats, `NaN`, `Infinity` | `42`, `3.14` |
| `boolean` | `true` or `false` | `true` |
| `bigint` | Large integers | `9007199254740993n` |
| `symbol` | Unique symbols | `Symbol("id")` |
| `null` | Intentional absence | `null` |
| `undefined` | Missing/uninitialized value | `undefined` |

Basic syntax:

```ts
let username: string = "evan";
let retryCount: number = 3;
let isAdmin: boolean = false;
let largeId: bigint = 12345678901234567890n;
let cacheKey: symbol = Symbol("cacheKey");
let deletedAt: null = null;
let middleName: undefined = undefined;
```

Practical example:

```ts
type UserSummary = {
  id: string;
  name: string;
  loginCount: number;
  emailVerified: boolean;
  deletedAt: string | null; // Common API shape: string date or null.
};
```

Best practices:

- Prefer precise primitives over broad types like `object` or `any`.
- With `strictNullChecks`, `null` and `undefined` are not assignable to everything. This is usually what you want.
- Use `string | null` when a value is intentionally empty; use `string | undefined` when it may be omitted.

### `any`

`any` disables type checking for a value. It is an escape hatch.

```ts
let response: any = await fetch("/api/user").then((res) => res.json());

response.name.toUpperCase();
response.profile.address.zip.toFixed();
// TypeScript allows all of this, even if it crashes at runtime.
```

Real-world use:

```ts
// Acceptable as a temporary migration step from JavaScript.
function legacyPluginHook(payload: any) {
  // TODO: replace any with a real plugin payload type.
  console.log(payload);
}
```

Warning: avoid `any` in application boundaries. It spreads quickly and weakens nearby code.

### `unknown`

`unknown` means “some value, but I must check it before using it.” It is safer than `any`.

```ts
let payload: unknown = await fetch("/api/session").then((res) => res.json());

// payload.userId; // Error: payload is unknown.

if (typeof payload === "object" && payload !== null && "userId" in payload) {
  // Still narrow carefully before trusting nested values.
  console.log(payload.userId);
}
```

Practical example:

```ts
function parseJson(value: string): unknown {
  return JSON.parse(value);
}

const data = parseJson('{"email":"user@example.com"}');

if (
  typeof data === "object" &&
  data !== null &&
  "email" in data &&
  typeof data.email === "string"
) {
  data.email.toLowerCase();
}
```

Best practice: use `unknown` for untrusted external data, then narrow or validate it.

### `never`

`never` represents values that cannot exist. It appears in functions that never return, impossible branches, and exhaustive checks.

```ts
function fail(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {
    // Never reaches the end.
  }
}
```

Exhaustiveness example:

```ts
type PaymentStatus = "pending" | "paid" | "failed";

function labelStatus(status: PaymentStatus): string {
  switch (status) {
    case "pending":
      return "Waiting";
    case "paid":
      return "Complete";
    case "failed":
      return "Problem";
    default: {
      const exhaustiveCheck: never = status;
      return exhaustiveCheck;
    }
  }
}
```

Warning: if a value unexpectedly becomes `never`, you may have narrowed it too far or created an impossible generic constraint.

### `void`

`void` means a function’s return value should not be used. It does not mean the same thing as `undefined` in all contexts.

```ts
function logEvent(name: string): void {
  console.log(name);
}

const result = logEvent("checkout_started");
// result has type void.
```

`void` vs. `undefined`:

```ts
function returnsUndefined(): undefined {
  return undefined; // Must specifically return undefined.
}

function returnsVoid(): void {
  return; // Return value is intentionally ignored.
}
```

Best practice: use `void` for callbacks and side-effect functions.

```ts
type ClickHandler = (eventName: string) => void;

const trackClick: ClickHandler = (eventName) => {
  console.log("tracked", eventName);
};
```

---
## 2. Type Annotations and Inference

Type annotations explicitly declare a type. Type inference lets TypeScript derive a type from the assigned value or usage.

### Type annotations

Basic syntax:

```ts
const productId: string = "prod_123";
let quantity: number = 1;
let couponCode: string | undefined;
```

Function annotations:

```ts
function formatPrice(cents: number, currency: string): string {
  return `${currency} ${(cents / 100).toFixed(2)}`;
}
```

Practical example:

```ts
type CreateOrderRequest = {
  productId: string;
  quantity: number;
};

async function createOrder(request: CreateOrderRequest): Promise<string> {
  const response = await fetch("/api/orders", {
    method: "POST",
    body: JSON.stringify(request),
  });

  const order: { id: string } = await response.json();
  return order.id;
}
```

### Type inference

TypeScript often knows the type without annotation.

```ts
const role = "admin";
// role is inferred as the literal type "admin" because const cannot be reassigned.

let status = "loading";
// status is inferred as string because let can be reassigned.

const retries = 3;
// retries is inferred as the literal type 3.
```

Inference from function return values:

```ts
function getInitials(name: string) {
  return name
    .split(" ")
    .map((part) => part[0])
    .join("");
  // Return type inferred as string.
}
```

Best practices:

- Let TypeScript infer obvious local variable types.
- Annotate function parameters, public function returns, exported constants, and API boundaries.
- Add return types to exported functions to prevent accidental API changes.

```ts
export function calculateDiscount(totalCents: number): number {
  return totalCents > 10_000 ? 0.15 : 0;
}
```

Common mistake:

```ts
const items = [];
// Depending on compiler options and context, this can infer any[] or never[].

const products: string[] = [];
products.push("Keyboard");
```

---
## 3. Arrays and Tuples

Arrays represent lists of values of the same type. Tuples represent fixed-position arrays where each position has a known type.

### Arrays

Basic syntax:

```ts
const userIds: string[] = ["u1", "u2"];
const scores: Array<number> = [10, 20, 30];
```

Array of objects:

```ts
type Notification = {
  id: string;
  read: boolean;
};

const notifications: Notification[] = [
  { id: "n1", read: false },
  { id: "n2", read: true },
];
```

Readonly arrays:

```ts
const permissions: readonly string[] = ["read", "write"];

// permissions.push("delete"); // Error: readonly array cannot be mutated.
```

Practical example:

```ts
function unreadCount(notifications: readonly Notification[]): number {
  return notifications.filter((notification) => !notification.read).length;
}
```

Best practice: accept `readonly T[]` when a function only reads an array.

### Tuples

A tuple has a fixed length and specific types by position.

```ts
const coordinates: [number, number] = [40.7128, -74.006];
const userEntry: [id: string, name: string, active: boolean] = ["u1", "Ada", true];
```

Optional tuple elements:

```ts
type SearchArgs = [query: string, limit?: number];

const basicSearch: SearchArgs = ["typescript"];
const limitedSearch: SearchArgs = ["typescript", 10];
```

Rest tuple elements:

```ts
type LogEntry = [level: "info" | "error", message: string, ...meta: unknown[]];

const entry: LogEntry = ["error", "Payment failed", { orderId: "ord_123" }];
```

Practical example:

```ts
function useToggle(initial: boolean): [value: boolean, toggle: () => void] {
  let value = initial;

  return [
    value,
    () => {
      value = !value;
    },
  ];
}
```

Best practices:

- Use arrays for variable-length homogeneous lists.
- Use tuples for fixed-position data like coordinates, React hooks, parser results, or command arguments.
- Prefer named tuple elements for readability.

---
## 4. Object Types

Object types describe the shape of JavaScript objects.

### Inline object types

Basic syntax:

```ts
function sendWelcomeEmail(user: { email: string; name: string }): void {
  console.log(`Sending email to ${user.email}`);
}
```

Good for one-off shapes. For repeated use, prefer a named type or interface.

### Optional properties

Use `?` for properties that may be omitted.

```ts
type UserProfile = {
  id: string;
  displayName: string;
  avatarUrl?: string;
};

const profile: UserProfile = {
  id: "u1",
  displayName: "Ada",
  // avatarUrl may be omitted.
};
```

Warning with optional properties:

```ts
function renderAvatar(profile: UserProfile): string {
  return profile.avatarUrl ?? "/default-avatar.png";
}
```

Best practice: distinguish optional from nullable.

```ts
type FormState = {
  middleName?: string; // Field may be absent.
  deletedAt: string | null; // Field is present, but may be null.
};
```

### `readonly` properties

`readonly` prevents reassignment through that type.

```ts
type ApiUser = {
  readonly id: string;
  email: string;
};

const user: ApiUser = { id: "u1", email: "user@example.com" };

// user.id = "u2"; // Error: cannot assign to readonly property.
user.email = "new@example.com";
```

Best practice: use `readonly` for IDs, timestamps, and immutable configuration.

### Index signatures

Index signatures describe objects with dynamic keys.

```ts
type FeatureFlags = {
  [flagName: string]: boolean;
};

const flags: FeatureFlags = {
  newCheckout: true,
  betaProfile: false,
};
```

More constrained example:

```ts
type Locale = "en" | "es" | "fr";

type Translations = {
  [locale in Locale]: string;
};

const labels: Translations = {
  en: "Save",
  es: "Guardar",
  fr: "Enregistrer",
};
```

Common mistake:

```ts
type BadConfig = {
  [key: string]: string;
  // retryCount: number; // Error: number is not assignable to string index type.
};
```

Best practice: prefer `Record<K, V>` or mapped types when keys are known.

---
## 5. Unions, Intersections, and Literals

These types combine or constrain possible values.

### Union types

A union means a value can be one of several types.

```ts
type Id = string | number;

function findUser(id: Id) {
  console.log("Finding user", id);
}
```

Practical example:

```ts
type ApiResult =
  | { ok: true; data: { id: string; email: string } }
  | { ok: false; error: string };

function handleResult(result: ApiResult): string {
  if (result.ok) {
    return result.data.email;
  }

  return result.error;
}
```

Best practice: narrow unions before using members that exist on only one branch.

```ts
function normalizeId(id: string | number): string {
  return typeof id === "string" ? id : id.toString();
}
```

### Intersection types

An intersection combines multiple types into one.

```ts
type Timestamped = {
  createdAt: string;
  updatedAt: string;
};

type Product = {
  id: string;
  name: string;
};

type ProductRecord = Product & Timestamped;
```

Practical example:

```ts
type AuthenticatedRequest = Request & {
  user: {
    id: string;
    role: "admin" | "member";
  };
};
```

Warning: intersections are not “either/or”; they require all properties.

```ts
type NeedsBoth = { email: string } & { phone: string };

const contact: NeedsBoth = {
  email: "user@example.com",
  phone: "+1-555-0100",
};
```

### Literal types

Literal types restrict values to exact strings, numbers, booleans, or bigint values.

```ts
type Theme = "light" | "dark" | "system";
type HttpStatus = 200 | 201 | 400 | 404 | 500;

const theme: Theme = "dark";
```

Practical example:

```ts
type Permission = "user:read" | "user:write" | "billing:read";

function canAccess(permission: Permission): boolean {
  return permission === "user:read";
}
```

Best practice: prefer string-literal unions for finite sets used in app logic.

---
## 6. Type Aliases and Interfaces

Type aliases and interfaces both name object shapes. They overlap heavily but have important differences.

### Type aliases

A type alias can name any type expression.

```ts
type UserId = string;

type ApiStatus = "idle" | "loading" | "success" | "error";

type User = {
  id: UserId;
  email: string;
};
```

Practical example:

```ts
type ApiResponse<T> =
  | { ok: true; data: T }
  | { ok: false; error: { message: string; code: string } };
```

### Interfaces

Interfaces describe object shapes and can be extended or merged.

```ts
interface Customer {
  id: string;
  email: string;
}

interface PremiumCustomer extends Customer {
  plan: "pro" | "enterprise";
}
```

Practical example:

```ts
interface Repository<T> {
  findById(id: string): Promise<T | null>;
  save(entity: T): Promise<void>;
}
```

### Interface vs. type alias

| Use case | Prefer |
|---|---|
| Object shape intended for extension | `interface` |
| Union, tuple, primitive alias, conditional type | `type` |
| Public library APIs that may be augmented | `interface` |
| App-level domain models | Either; be consistent |
| Mapped or template literal types | `type` |

Warnings:

```ts
interface UserSettings {
  theme: "light" | "dark";
}

interface UserSettings {
  locale: string;
}

// Interfaces merge. UserSettings now has both theme and locale.
const settings: UserSettings = {
  theme: "dark",
  locale: "en-US",
};
```

```ts
type Account = {
  id: string;
};

// type Account = { email: string }; // Error: duplicate identifier.
```

Best practice: use `type` for unions and type-level programming; use `interface` when declaration merging or class implementation matters.

---
## 7. Function Types

Function types describe parameter and return types.

### Function declarations

```ts
function getDisplayName(firstName: string, lastName: string): string {
  return `${firstName} ${lastName}`;
}
```

### Function type expressions

```ts
type Formatter = (value: number) => string;

const formatCents: Formatter = (value) => `$${(value / 100).toFixed(2)}`;
```

Object method signatures:

```ts
type CartService = {
  addItem(productId: string, quantity: number): void;
  removeItem: (productId: string) => void;
};
```

### Optional parameters

```ts
function searchProducts(query: string, limit?: number): void {
  console.log(query, limit ?? 20);
}

searchProducts("keyboard");
searchProducts("keyboard", 10);
```

Best practice: optional parameters usually belong after required parameters.

### Default parameters

```ts
function createPageUrl(page: number = 1): string {
  return `/products?page=${page}`;
}
```

Default parameters are inferred from the default value unless annotated.

```ts
function requestJson(path: string, method: "GET" | "POST" = "GET") {
  return fetch(path, { method });
}
```

### Rest parameters

```ts
function logAuditEvent(eventName: string, ...tags: string[]): void {
  console.log(eventName, tags.join(","));
}

logAuditEvent("login", "security", "user");
```

Tuple rest parameters:

```ts
type EventArgs = [eventName: string, userId: string, metadata?: object];

function trackEvent(...args: EventArgs): void {
  const [eventName, userId, metadata] = args;
  console.log(eventName, userId, metadata);
}
```

### `this` types in functions

You can type `this` as a fake first parameter. It is not passed at runtime.

```ts
type Button = {
  label: string;
  clickCount: number;
};

function handleButtonClick(this: Button): void {
  this.clickCount += 1;
  console.log(`${this.label} clicked`);
}

const saveButton: Button = { label: "Save", clickCount: 0 };
handleButtonClick.call(saveButton);
```

Callbacks can forbid `this` usage:

```ts
type SafeCallback = (this: void, value: string) => void;

const callback: SafeCallback = (value) => {
  console.log(value);
  // this; // Error with noImplicitThis / strict settings.
};
```

Best practices:

- Prefer arrow functions for lexical `this`.
- Use explicit `this` parameters when typing legacy JS APIs, event emitters, or plugin systems.
- Avoid returning `any` from function types. Use generics or `unknown` instead.

---
## 8. Generics

Generics let types accept parameters. They are reusable type variables.

### Basic generics

```ts
function identity<T>(value: T): T {
  return value;
}

const id = identity("user_123");
// id is string.
```

Practical example:

```ts
type ApiResponse<TData> = {
  data: TData;
  requestId: string;
};

async function getJson<TData>(url: string): Promise<TData> {
  const response = await fetch(url);
  return response.json() as Promise<TData>;
}

type User = { id: string; email: string };

const user = await getJson<User>("/api/me");
```

Warning: generic type arguments can lie when you assert unvalidated external data. Runtime validation is still needed for untrusted APIs.

### Generic constraints

Use `extends` to require that a generic has a minimum shape.

```ts
function getId<T extends { id: string }>(entity: T): string {
  return entity.id;
}

getId({ id: "u1", email: "user@example.com" });
```

Practical example:

```ts
function sortByCreatedAt<T extends { createdAt: string }>(items: T[]): T[] {
  return [...items].sort((a, b) => a.createdAt.localeCompare(b.createdAt));
}
```

### Generic defaults

Provide a default type when callers omit one.

```ts
type PaginatedResult<TItem, TMeta = { total: number }> = {
  items: TItem[];
  meta: TMeta;
};

type ProductPage = PaginatedResult<{ id: string; name: string }>;
```

### Generic keys

`keyof` and generics often work together.

```ts
function getProperty<TObject, TKey extends keyof TObject>(
  object: TObject,
  key: TKey,
): TObject[TKey] {
  return object[key];
}

const account = { id: "a1", plan: "pro", seats: 5 };
const seats = getProperty(account, "seats");
// seats is number.
```

Best practices:

- Use descriptive generic names when helpful: `TUser`, `TData`, `TError`.
- Use single letters for common low-level helpers: `T`, `K`, `V`.
- Do not add generics that do not preserve or relate types.

```ts
// Bad: T does not improve the type relationship.
function parseBad<T>(value: string): T {
  return JSON.parse(value);
}

// Better: return unknown and validate or narrow.
function parseSafe(value: string): unknown {
  return JSON.parse(value);
}
```

---
## 9. TypeScript Type Operators

Type operators create new types from existing values and types.

### `keyof`

`keyof T` creates a union of property names of `T`.

```ts
type User = {
  id: string;
  email: string;
  role: "admin" | "member";
};

type UserKey = keyof User;
// "id" | "email" | "role"
```

Practical example:

```ts
function pluck<TObject, TKey extends keyof TObject>(
  items: TObject[],
  key: TKey,
): TObject[TKey][] {
  return items.map((item) => item[key]);
}
```

Best practice: use `keyof` to avoid hard-coded string keys drifting from object types.

### `typeof`

In a type position, `typeof` extracts the type of a value.

```ts
const defaultConfig = {
  retries: 3,
  mode: "production",
};

type AppConfig = typeof defaultConfig;
// { retries: number; mode: string }
```

Practical example:

```ts
const routes = {
  home: "/",
  account: "/account",
  billing: "/billing",
} as const;

type RouteName = keyof typeof routes;
// "home" | "account" | "billing"

type RoutePath = (typeof routes)[RouteName];
// "/" | "/account" | "/billing"
```

Warning: JavaScript `typeof value` at runtime and TypeScript `typeof value` in type position are related but not identical use cases.

### `in`

`in` has two common type-system uses: narrowing and mapped types.

Runtime narrowing:

```ts
type Success = { data: string };
type Failure = { error: string };

function readResult(result: Success | Failure): string {
  if ("data" in result) {
    return result.data;
  }

  return result.error;
}
```

Mapped type iteration:

```ts
type Flags<T> = {
  [Key in keyof T]: boolean;
};

type UserFlags = Flags<{ email: string; active: boolean }>;
// { email: boolean; active: boolean }
```

### `as`

`as` has multiple meanings depending on context.

Type assertion:

```ts
const input = document.querySelector("input") as HTMLInputElement;
console.log(input.value);
```

Key remapping in mapped types:

```ts
type Getters<T> = {
  [Key in keyof T as `get${Capitalize<string & Key>}`]: () => T[Key];
};

type UserGetters = Getters<{ id: string; email: string }>;
// { getId: () => string; getEmail: () => string }
```

Warning: `as` does not change runtime values. It only tells TypeScript to treat a value as another type.

### `satisfies`

`satisfies` checks that a value matches a type without widening the value more than necessary.

```ts
type RouteConfig = Record<string, { path: string; requiresAuth: boolean }>;

const routes = {
  home: { path: "/", requiresAuth: false },
  dashboard: { path: "/dashboard", requiresAuth: true },
} satisfies RouteConfig;

// routes.dashboard.requiresAuth remains the literal true, not just boolean.
```

Practical example:

```ts
type Permission = "read" | "write" | "delete";

type RolePermissions = Record<string, readonly Permission[]>;

const rolePermissions = {
  admin: ["read", "write", "delete"],
  editor: ["read", "write"],
  viewer: ["read"],
} as const satisfies RolePermissions;
```

Warning: `satisfies` checks compatibility but does not force the variable’s type to become the target type.

```ts
const config = {
  mode: "dark",
  retries: 3,
} satisfies { mode: string; retries: number };

// config.mode is still inferred from the object expression, not simply replaced everywhere by string.
```

### `infer`

`infer` introduces a type variable inside a conditional type.

```ts
type ArrayItem<T> = T extends readonly (infer Item)[] ? Item : never;

type Product = ArrayItem<Array<{ id: string; name: string }>>;
// { id: string; name: string }
```

Practical example:

```ts
type PromiseValue<T> = T extends Promise<infer Value> ? Value : T;

type User = PromiseValue<Promise<{ id: string }>>;
// { id: string }
```

Best practice: use `infer` for type extraction, not for simple cases where indexed access is clearer.

---
## 10. Type Assertions and Const Assertions

Assertions tell TypeScript more specific type information. They do not perform runtime checks.

### Type assertions

Basic syntax:

```ts
const value: unknown = "hello";
const length = (value as string).length;
```

DOM example:

```ts
const emailInput = document.querySelector("#email") as HTMLInputElement | null;

if (emailInput) {
  emailInput.value = "user@example.com";
}
```

Warning: assertion vs. narrowing:

```ts
const rawValue: unknown = 123;

// Dangerous: compiles, but crashes at runtime.
const upper = (rawValue as string).toUpperCase();

// Safer: narrow first.
if (typeof rawValue === "string") {
  rawValue.toUpperCase();
}
```

Double assertion:

```ts
const valueFromLegacyCode = "user_123" as unknown as { id: string };
// Avoid this unless bridging a truly untyped boundary.
```

Best practices:

- Prefer narrowing, validation, or better source types over assertions.
- Keep assertions close to the boundary where TypeScript lacks information.
- Avoid asserting API responses without validation when security or correctness matters.

### Const assertions: `as const`

`as const` makes literals deeply readonly and preserves exact literal types.

```ts
const status = "success" as const;
// type is "success", not string.

const button = {
  variant: "primary",
  size: "sm",
} as const;
// { readonly variant: "primary"; readonly size: "sm" }
```

Practical example:

```ts
const events = ["user.created", "user.deleted", "invoice.paid"] as const;

type EventName = (typeof events)[number];
// "user.created" | "user.deleted" | "invoice.paid"
```

Warning: `as const` can make data readonly in ways that surprise you.

```ts
const mutableTags = ["new", "sale"];
mutableTags.push("featured");

const readonlyTags = ["new", "sale"] as const;
// readonlyTags.push("featured"); // Error.
```

Best practice: use `as const` for config objects, action names, route maps, permissions, and fixed value lists.

---
## 11. Type Narrowing and Type Guards

Narrowing is how TypeScript refines a broad type into a more specific type based on control flow.

### Common narrowing techniques

| Technique | Example |
|---|---|
| `typeof` | `typeof value === "string"` |
| `instanceof` | `error instanceof Error` |
| Truthiness | `if (value) { ... }` |
| Equality | `status === "success"` |
| `in` operator | `"data" in result` |
| Discriminant property | `event.type === "click"` |
| User-defined type guard | `isUser(value)` |

### `typeof` narrowing

```ts
function formatId(id: string | number): string {
  if (typeof id === "number") {
    return id.toString();
  }

  return id.toUpperCase();
}
```

### `instanceof` narrowing

```ts
function errorMessage(error: unknown): string {
  if (error instanceof Error) {
    return error.message;
  }

  return "Unknown error";
}
```

### Truthiness narrowing

```ts
function displayName(name: string | null | undefined): string {
  if (name) {
    return name;
  }

  return "Anonymous";
}
```

Warning: truthiness removes empty strings, `0`, and `false`, not just `null`/`undefined`.

```ts
function formatQuantity(quantity: number | null): string {
  if (quantity !== null) {
    return quantity.toString(); // Keeps 0 valid.
  }

  return "Not selected";
}
```

### User-defined type guards

A type guard returns a type predicate: `value is SomeType`.

```ts
type User = {
  id: string;
  email: string;
};

function isUser(value: unknown): value is User {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "email" in value &&
    typeof value.id === "string" &&
    typeof value.email === "string"
  );
}

const payload: unknown = await fetch("/api/me").then((res) => res.json());

if (isUser(payload)) {
  payload.email.toLowerCase();
}
```

### Assertion functions

Assertion functions throw if a condition is not met and narrow afterward.

```ts
function assertIsString(value: unknown): asserts value is string {
  if (typeof value !== "string") {
    throw new Error("Expected string");
  }
}

const input: unknown = "abc";
assertIsString(input);
input.toUpperCase(); // input is string here.
```

Best practices:

- Prefer narrowing over type assertions.
- Validate untrusted data at boundaries.
- Keep type guards small and testable.

---
## 12. Discriminated Unions

A discriminated union is a union where each variant has a shared literal property, often named `type`, `kind`, or `status`.

Basic syntax:

```ts
type LoadingState = { status: "loading" };
type SuccessState = { status: "success"; data: string[] };
type ErrorState = { status: "error"; error: string };

type ProductsState = LoadingState | SuccessState | ErrorState;
```

Example:

```ts
function renderProducts(state: ProductsState): string {
  switch (state.status) {
    case "loading":
      return "Loading products...";
    case "success":
      return `Found ${state.data.length} products`;
    case "error":
      return state.error;
  }
}
```

Real-world API example:

```ts
type PaymentEvent =
  | { type: "payment.created"; paymentId: string; amountCents: number }
  | { type: "payment.failed"; paymentId: string; reason: string }
  | { type: "payment.refunded"; paymentId: string; refundId: string };

function handlePaymentEvent(event: PaymentEvent): void {
  switch (event.type) {
    case "payment.created":
      console.log(event.amountCents);
      break;
    case "payment.failed":
      console.log(event.reason);
      break;
    case "payment.refunded":
      console.log(event.refundId);
      break;
    default: {
      const exhaustive: never = event;
      throw new Error(`Unhandled event: ${JSON.stringify(exhaustive)}`);
    }
  }
}
```

Best practices:

- Use a consistent discriminant name such as `type` or `status`.
- Use exhaustive `never` checks in reducers, event handlers, and state machines.
- Avoid optional discriminants; every variant should have the discriminant.

---
## 13. Enums

Enums define named constants. TypeScript supports numeric and string enums, but union literals are often simpler in modern application code.

### Numeric enums

```ts
enum HttpStatusCode {
  Ok = 200,
  Created = 201,
  BadRequest = 400,
  NotFound = 404,
}

const statusCode: HttpStatusCode = HttpStatusCode.Ok;
```

### String enums

```ts
enum UserRole {
  Admin = "admin",
  Member = "member",
  Guest = "guest",
}

function canManageUsers(role: UserRole): boolean {
  return role === UserRole.Admin;
}
```

### Enum alternative: union literals

```ts
type UserRole = "admin" | "member" | "guest";

const roles = {
  Admin: "admin",
  Member: "member",
  Guest: "guest",
} as const;

type RoleValue = (typeof roles)[keyof typeof roles];
```

Enums vs. union literals:

| Use case | Consider |
|---|---|
| Public API with named runtime object | `enum` or `as const` object |
| App-only finite string states | Union literals |
| Need zero runtime output | Union literals |
| Need interop with existing enum API | `enum` |

Warnings:

- Numeric enums can be less strict than expected in some cases.
- `const enum` can cause build-tool issues when transpilers do not understand TypeScript’s emit behavior.
- Union literals compose better with template literal types and mapped types.

Best practice: prefer union literals or `as const` objects for most app-level string states.

---
## 14. Utility Types

Utility types are built-in generic helpers for common type transformations.

### Quick reference

| Utility | Purpose |
|---|---|
| `Partial<T>` | Make all properties optional |
| `Required<T>` | Make all properties required |
| `Readonly<T>` | Make all properties readonly |
| `Pick<T, K>` | Select some properties |
| `Omit<T, K>` | Remove some properties |
| `Record<K, V>` | Object with keys `K` and values `V` |
| `Exclude<T, U>` | Remove union members assignable to `U` |
| `Extract<T, U>` | Keep union members assignable to `U` |
| `NonNullable<T>` | Remove `null` and `undefined` |
| `ReturnType<T>` | Get function return type |
| `Parameters<T>` | Get function parameter tuple |
| `ConstructorParameters<T>` | Get constructor parameter tuple |
| `InstanceType<T>` | Get instance type from constructor |
| `Awaited<T>` | Recursively unwrap promises |

Shared model:

```ts
type User = {
  id: string;
  email: string;
  name: string;
  role: "admin" | "member";
  createdAt: string;
};
```

### `Partial<T>`

Makes every property optional.

```ts
type UserPatch = Partial<User>;

const patch: UserPatch = {
  name: "Grace Hopper",
};
```

Practical example:

```ts
function updateUser(id: string, patch: Partial<User>): void {
  console.log("Updating", id, patch);
}
```

Warning: `Partial<T>` is shallow. Nested objects are not deeply partial.

### `Required<T>`

Makes every property required.

```ts
type DraftProfile = {
  name?: string;
  avatarUrl?: string;
};

type CompleteProfile = Required<DraftProfile>;

const profile: CompleteProfile = {
  name: "Ada",
  avatarUrl: "/ada.png",
};
```

### `Readonly<T>`

Makes every property readonly.

```ts
type ReadonlyUser = Readonly<User>;

const user: ReadonlyUser = {
  id: "u1",
  email: "user@example.com",
  name: "User",
  role: "member",
  createdAt: "2026-01-01T00:00:00Z",
};

// user.email = "new@example.com"; // Error.
```

Warning: `Readonly<T>` is shallow.

### `Pick<T, K>`

Selects specific properties.

```ts
type UserPreview = Pick<User, "id" | "name">;

const preview: UserPreview = {
  id: "u1",
  name: "Ada",
};
```

### `Omit<T, K>`

Removes specific properties.

```ts
type PublicUser = Omit<User, "role" | "createdAt">;

const publicUser: PublicUser = {
  id: "u1",
  email: "user@example.com",
  name: "Ada",
};
```

Practical example:

```ts
type CreateUserInput = Omit<User, "id" | "createdAt">;
```

### `Record<K, V>`

Creates an object type with keys `K` and values `V`.

```ts
type Role = "admin" | "member" | "guest";

type RoleLabels = Record<Role, string>;

const labels: RoleLabels = {
  admin: "Administrator",
  member: "Member",
  guest: "Guest",
};
```

Best practice: use `Record` for complete maps over known key unions.

### `Exclude<T, U>`

Removes union members from `T` that are assignable to `U`.

```ts
type Status = "idle" | "loading" | "success" | "error";
type FinishedStatus = Exclude<Status, "idle" | "loading">;
// "success" | "error"
```

### `Extract<T, U>`

Keeps union members from `T` that are assignable to `U`.

```ts
type Event =
  | { type: "user.created"; userId: string }
  | { type: "invoice.paid"; invoiceId: string }
  | { type: "invoice.failed"; invoiceId: string };

type InvoiceEvent = Extract<Event, { type: `invoice.${string}` }>;
```

### `NonNullable<T>`

Removes `null` and `undefined`.

```ts
type MaybeEmail = string | null | undefined;
type Email = NonNullable<MaybeEmail>;
// string
```

Practical example:

```ts
function requireValue<T>(value: T): NonNullable<T> {
  if (value === null || value === undefined) {
    throw new Error("Expected value");
  }

  return value;
}
```

### `ReturnType<T>`

Extracts a function’s return type.

```ts
function createSession() {
  return {
    token: "abc",
    expiresAt: Date.now() + 3600,
  };
}

type Session = ReturnType<typeof createSession>;
```

### `Parameters<T>`

Extracts a function’s parameters as a tuple.

```ts
function track(eventName: string, metadata?: Record<string, unknown>): void {
  console.log(eventName, metadata);
}

type TrackArgs = Parameters<typeof track>;
// [eventName: string, metadata?: Record<string, unknown> | undefined]

const args: TrackArgs = ["signup", { plan: "pro" }];
```

### `ConstructorParameters<T>`

Extracts constructor parameters as a tuple.

```ts
class ApiClient {
  constructor(public baseUrl: string, public timeoutMs: number) {}
}

type ApiClientArgs = ConstructorParameters<typeof ApiClient>;
// [baseUrl: string, timeoutMs: number]
```

### `InstanceType<T>`

Extracts the instance type created by a constructor.

```ts
class Logger {
  info(message: string): void {
    console.log(message);
  }
}

type LoggerInstance = InstanceType<typeof Logger>;
```

### `Awaited<T>`

Recursively unwraps promises.

```ts
type UserPromise = Promise<Promise<{ id: string }>>;
type ResolvedUser = Awaited<UserPromise>;
// { id: string }
```

Practical example:

```ts
async function fetchSettings() {
  return { theme: "dark" as const, locale: "en-US" };
}

type Settings = Awaited<ReturnType<typeof fetchSettings>>;
```

Best practices:

- Combine utility types to model API inputs and outputs.
- Avoid excessive nested utilities that are hard to read; name intermediate types.

```ts
type UserEditableFields = Pick<User, "email" | "name">;
type UpdateUserRequest = Partial<UserEditableFields>;
```

---
## 15. Mapped Types

Mapped types create new object types by iterating over keys.

Basic syntax:

```ts
type OptionsFlags<T> = {
  [Key in keyof T]: boolean;
};

type FeatureConfig = {
  search: () => void;
  checkout: () => void;
};

type EnabledFeatures = OptionsFlags<FeatureConfig>;
// { search: boolean; checkout: boolean }
```

### Mapping value types

```ts
type Nullable<T> = {
  [Key in keyof T]: T[Key] | null;
};

type UserFormValues = Nullable<{
  email: string;
  age: number;
}>;
// { email: string | null; age: number | null }
```

### Mapping modifiers

Add or remove `readonly` and optional modifiers.

```ts
type Mutable<T> = {
  -readonly [Key in keyof T]: T[Key];
};

type RequiredFields<T> = {
  [Key in keyof T]-?: T[Key];
};
```

Practical example:

```ts
type FormErrors<TForm> = {
  [Field in keyof TForm]?: string;
};

type SignupForm = {
  email: string;
  password: string;
};

const errors: FormErrors<SignupForm> = {
  email: "Enter a valid email",
};
```

### Key remapping with `as`

```ts
type EventHandlers<TEvents extends string> = {
  [EventName in TEvents as `on${Capitalize<EventName>}`]: () => void;
};

type ModalHandlers = EventHandlers<"open" | "close">;
// { onOpen: () => void; onClose: () => void }
```

Best practices:

- Use mapped types to avoid duplicating parallel shapes like values/errors/touched fields.
- Name mapped types clearly; advanced transformations can become unreadable quickly.

---
## 16. Conditional Types

Conditional types choose one type or another based on assignability.

Basic syntax:

```ts
type IsString<T> = T extends string ? true : false;

type A = IsString<"hello">; // true
type B = IsString<42>; // false
```

Practical example:

```ts
type ApiData<TResponse> = TResponse extends { data: infer TData } ? TData : never;

type UserData = ApiData<{ data: { id: string; email: string } }>;
// { id: string; email: string }
```

### Conditional types distribute over unions

```ts
type ToArray<T> = T extends unknown ? T[] : never;

type Result = ToArray<string | number>;
// string[] | number[]
```

Prevent distribution by wrapping each side in a tuple:

```ts
type ToArrayNonDistributive<T> = [T] extends [unknown] ? T[] : never;

type Result = ToArrayNonDistributive<string | number>;
// (string | number)[]
```

### Real-world example: async result extraction

```ts
type AsyncFunction = (...args: any[]) => Promise<unknown>;

type AsyncReturn<TFunction extends AsyncFunction> =
  TFunction extends (...args: any[]) => Promise<infer TResult> ? TResult : never;

async function loadUser() {
  return { id: "u1", email: "user@example.com" };
}

type LoadedUser = AsyncReturn<typeof loadUser>;
```

Warnings:

- Conditional types can become difficult to debug when heavily nested.
- Distribution over unions is powerful but surprising.
- Prefer built-in utilities like `ReturnType`, `Parameters`, and `Awaited` when they fit.

---
## 17. Template Literal Types

Template literal types build string types from other string types.

Basic syntax:

```ts
type Size = "sm" | "md" | "lg";
type Variant = "primary" | "secondary";

type ButtonClass = `button-${Variant}-${Size}`;
// "button-primary-sm" | "button-primary-md" | ...
```

Practical example: event names from object keys.

```ts
type User = {
  email: string;
  role: "admin" | "member";
};

type UserChangeEvent = `${string & keyof User}Changed`;
// "emailChanged" | "roleChanged"
```

Type-safe watcher:

```ts
type Watchable<T> = {
  on<Key extends string & keyof T>(
    eventName: `${Key}Changed`,
    callback: (newValue: T[Key]) => void,
  ): void;
};

declare const userWatcher: Watchable<User>;

userWatcher.on("emailChanged", (email) => {
  email.toLowerCase(); // email is string.
});
```

Intrinsic string manipulation types:

```ts
type EventName = "user_created";

type Upper = Uppercase<EventName>; // "USER_CREATED"
type Lower = Lowercase<"USER_CREATED">; // "user_created"
type Capital = Capitalize<"user">; // "User"
type Uncapital = Uncapitalize<"User">; // "user"
```

Best practices:

- Use template literal types for event names, route names, permission strings, CSS class names, and generated API keys.
- Avoid generating enormous unions; they can slow down type checking.

---
## 18. Recursive Types

Recursive types reference themselves. They are useful for trees, nested JSON, menus, comments, and file systems.

Basic syntax:

```ts
type TreeNode = {
  id: string;
  children: TreeNode[];
};
```

Practical example: nested comments.

```ts
type CommentNode = {
  id: string;
  author: string;
  body: string;
  replies: CommentNode[];
};

function countComments(comment: CommentNode): number {
  return 1 + comment.replies.reduce((total, reply) => total + countComments(reply), 0);
}
```

JSON value type:

```ts
type JsonValue =
  | string
  | number
  | boolean
  | null
  | JsonValue[]
  | { [key: string]: JsonValue };

const config: JsonValue = {
  theme: "dark",
  features: ["search", "billing"],
};
```

Recursive generic example:

```ts
type DeepReadonly<T> = {
  readonly [Key in keyof T]: T[Key] extends object ? DeepReadonly<T[Key]> : T[Key];
};
```

Warning: recursive utility types can be expensive or overly broad. Arrays, functions, dates, and maps often need special handling.

Best practice: keep recursive types focused on the actual domain shape.

---
## 19. Branded Types

Branded types create nominal-like distinctions between values that have the same runtime representation.

Basic syntax:

```ts
type Brand<TValue, TBrand extends string> = TValue & { readonly __brand: TBrand };

type UserId = Brand<string, "UserId">;
type OrderId = Brand<string, "OrderId">;
```

Example:

```ts
function toUserId(value: string): UserId {
  // Validate format here if needed.
  return value as UserId;
}

function getUser(id: UserId): void {
  console.log("Loading user", id);
}

const userId = toUserId("user_123");
getUser(userId);

const orderId = "order_123" as OrderId;
// getUser(orderId); // Error: OrderId is not UserId.
```

Practical example: validated email.

```ts
type EmailAddress = Brand<string, "EmailAddress">;

function parseEmail(value: string): EmailAddress | null {
  return value.includes("@") ? (value as EmailAddress) : null;
}

const email = parseEmail("user@example.com");

if (email) {
  sendEmail(email);
}

function sendEmail(to: EmailAddress): void {
  console.log("Sending to", to);
}
```

Best practices:

- Use branded types for IDs, validated strings, currencies, units, and security-sensitive values.
- Create brands through parsing or factory functions.
- Do not scatter `as Brand` assertions throughout the codebase.

---
## 20. Declaration Merging

Declaration merging lets TypeScript combine multiple declarations with the same name. This mainly applies to interfaces and namespaces.

### Interface merging

```ts
interface Window {
  analytics: {
    track(eventName: string): void;
  };
}

window.analytics.track("page_view");
```

Multiple declarations merge:

```ts
interface AppConfig {
  apiBaseUrl: string;
}

interface AppConfig {
  releaseVersion: string;
}

const config: AppConfig = {
  apiBaseUrl: "https://api.example.com",
  releaseVersion: "1.2.3",
};
```

Practical example: Express request augmentation.

```ts
declare global {
  namespace Express {
    interface Request {
      user?: {
        id: string;
        role: "admin" | "member";
      };
    }
  }
}
```

Warning: declaration merging can be surprising because declarations in different files combine globally.

Best practices:

- Use declaration merging for library augmentation and global objects.
- Keep augmentations in obvious files such as `global.d.ts` or `express.d.ts`.
- Prefer normal imports/exports for app types when merging is not needed.

---
## 21. Module Typing Basics

Modules need clear import/export types, especially at package and API boundaries.

### Exporting types

```ts
export type User = {
  id: string;
  email: string;
};

export interface UserRepository {
  findById(id: string): Promise<User | null>;
}
```

### Importing types

```ts
import type { User, UserRepository } from "./users";

export async function loadUser(repository: UserRepository, id: string): Promise<User | null> {
  return repository.findById(id);
}
```

Best practice: use `import type` for imports used only as types. This helps preserve clean runtime module output.

### Typing default and named exports

```ts
export default function formatDate(date: Date): string {
  return date.toISOString().slice(0, 10);
}

export type DateFormat = "short" | "long";
```

### Ambient module declarations

Use declarations for modules without bundled types.

```ts
declare module "legacy-datepicker" {
  export type DatepickerOptions = {
    format?: string;
    minDate?: Date;
  };

  export function createDatepicker(
    element: HTMLElement,
    options?: DatepickerOptions,
  ): void;
}
```

### Global declarations

```ts
declare global {
  interface Window {
    appVersion: string;
  }
}

export {};
```

The `export {}` makes the file a module so the global augmentation is scoped correctly.

Best practices:

- Keep `.d.ts` files for declarations only; avoid runtime code there.
- Prefer package-provided types or official `@types/*` packages when available.
- Use `unknown` at module boundaries when values are not validated.

---
## 22. React Typing Basics

React TypeScript mostly means typing props, events, children, refs, and reusable component APIs.

### Typing props

```ts
type ButtonProps = {
  label: string;
  variant?: "primary" | "secondary";
  disabled?: boolean;
  onClick: () => void;
};

function Button({ label, variant = "primary", disabled = false, onClick }: ButtonProps) {
  return (
    <button className={`button-${variant}`} disabled={disabled} onClick={onClick}>
      {label}
    </button>
  );
}
```

Best practice: let the function return type infer unless exporting a library API that needs explicitness.

### Typing children

```ts
import type { ReactNode } from "react";

type CardProps = {
  title: string;
  children: ReactNode;
};

function Card({ title, children }: CardProps) {
  return (
    <section>
      <h2>{title}</h2>
      {children}
    </section>
  );
}
```

Warning: `ReactNode` is for renderable content. It is broader than `JSX.Element`.

### Typing event handlers

```ts
import type { ChangeEvent, FormEvent } from "react";

function SignupForm() {
  function handleEmailChange(event: ChangeEvent<HTMLInputElement>) {
    console.log(event.currentTarget.value);
  }

  function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault();
  }

  return (
    <form onSubmit={handleSubmit}>
      <input type="email" onChange={handleEmailChange} />
    </form>
  );
}
```

### Reusing native element props

```ts
import type { ComponentPropsWithoutRef } from "react";

type IconButtonProps = ComponentPropsWithoutRef<"button"> & {
  icon: "save" | "delete";
  label: string;
};

function IconButton({ icon, label, ...buttonProps }: IconButtonProps) {
  return (
    <button {...buttonProps} aria-label={label}>
      {icon}
    </button>
  );
}
```

### Generic components

```ts
type SelectProps<TOption extends string> = {
  value: TOption;
  options: readonly TOption[];
  onChange: (value: TOption) => void;
};

function Select<TOption extends string>({ value, options, onChange }: SelectProps<TOption>) {
  return (
    <select value={value} onChange={(event) => onChange(event.currentTarget.value as TOption)}>
      {options.map((option) => (
        <option key={option} value={option}>
          {option}
        </option>
      ))}
    </select>
  );
}
```

Warning: DOM values are strings at runtime, so generic select components often need parsing or careful assertions.

Best practices:

- Prefer explicit props types over `React.FC`; it can obscure `children` and generics.
- Use `ComponentPropsWithoutRef<"button">` or similar helpers to wrap native elements.
- Keep component props serializable and narrow when used across app boundaries.

---
## 23. Type-Related Compiler Options

Compiler options shape how strict and useful TypeScript is.

### Recommended strictness options

| Option | Why it matters |
|---|---|
| `strict` | Enables the main strict type-checking family. |
| `noImplicitAny` | Errors when a type would silently become `any`. |
| `strictNullChecks` | Makes `null` and `undefined` explicit. |
| `strictFunctionTypes` | Checks function parameter variance more safely. |
| `noImplicitThis` | Errors when `this` has type `any`. |
| `useUnknownInCatchVariables` | Types `catch (error)` as `unknown`. |
| `exactOptionalPropertyTypes` | Treats optional properties more precisely. |
| `noUncheckedIndexedAccess` | Adds `undefined` when indexing arrays/objects. |
| `noPropertyAccessFromIndexSignature` | Requires bracket access for index-signature properties. |
| `noImplicitOverride` | Requires `override` on subclass overrides. |

Example:

```ts
// With noUncheckedIndexedAccess:
const names = ["Ada", "Grace"];
const first = names[0];
// first is string | undefined, because the array could be empty.
```

```ts
// With useUnknownInCatchVariables:
try {
  throw new Error("Failed");
} catch (error) {
  if (error instanceof Error) {
    console.error(error.message);
  }
}
```

### Module and emit-related options that affect types

| Option | Practical note |
|---|---|
| `isolatedModules` | Useful when Babel, SWC, esbuild, or other single-file transpilers compile TS. |
| `verbatimModuleSyntax` | Preserves import/export intent; pairs well with `import type`. |
| `moduleResolution` | Controls how imports resolve; often `bundler`, `node16`, or `nodenext`. |
| `jsx` | Controls JSX emit for React or other JSX runtimes. |
| `skipLibCheck` | Speeds builds by skipping declaration-file checking; can hide dependency type issues. |

Example `tsconfig` fragment:

```ts
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "useUnknownInCatchVariables": true,
    "isolatedModules": true,
    "verbatimModuleSyntax": true
  }
}
```

Best practices:

- Start new projects with `strict: true`.
- Add stricter options gradually in older codebases.
- Avoid solving compiler errors by adding `any`; narrow, validate, or improve the model.

---
## 24. Common Mistakes and Best Practices

### Prefer `unknown` over `any` for untrusted values

```ts
function handleWebhook(payload: unknown): void {
  if (
    typeof payload === "object" &&
    payload !== null &&
    "type" in payload &&
    typeof payload.type === "string"
  ) {
    console.log(payload.type);
  }
}
```

Use `any` only when intentionally opting out of type checking, ideally at a narrow migration boundary.

### Do not confuse type assertions with runtime validation

```ts
type User = { id: string; email: string };

const user = JSON.parse('{"id":123}') as User;
// Compiles, but user.id is actually a number at runtime.
```

Better:

```ts
function isUser(value: unknown): value is User {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "email" in value &&
    typeof value.id === "string" &&
    typeof value.email === "string"
  );
}
```

### Be careful with optional properties

```ts
type Preferences = {
  theme?: "light" | "dark";
};

function getTheme(preferences: Preferences): "light" | "dark" {
  return preferences.theme ?? "light";
}
```

With `exactOptionalPropertyTypes`, `theme?: T` means the property may be absent; it does not automatically mean `theme: undefined` should be assigned.

### Keep unions discriminated

Avoid vague unions:

```ts
type BadState = {
  loading?: boolean;
  data?: string[];
  error?: string;
};
```

Prefer explicit states:

```ts
type GoodState =
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; error: string };
```

### Avoid overly broad object types

```ts
function printKeys(value: object): void {
  console.log(Object.keys(value));
}

// object does not mean "any object with any property I want".
```

Prefer precise shapes:

```ts
function printUser(user: { id: string; email: string }): void {
  console.log(user.id, user.email);
}
```

### Use `satisfies` for config objects

```ts
type AppRoute = {
  path: string;
  title: string;
  requiresAuth: boolean;
};

const routes = {
  home: { path: "/", title: "Home", requiresAuth: false },
  account: { path: "/account", title: "Account", requiresAuth: true },
} as const satisfies Record<string, AppRoute>;
```

This checks the object shape while preserving literal information.

### Prefer union literals over enums for many app states

```ts
type ToastKind = "success" | "error" | "info";

function showToast(kind: ToastKind, message: string): void {
  console.log(kind, message);
}
```

Use enums when you specifically need a runtime enum object or are matching an existing API.

### Add return types to exported functions

```ts
export function buildInvoiceUrl(invoiceId: string): string {
  return `/invoices/${invoiceId}`;
}
```

This prevents accidental exported API changes.

### Use exhaustive checks with `never`

```ts
type Action =
  | { type: "increment" }
  | { type: "decrement" }
  | { type: "reset"; value: number };

function reducer(count: number, action: Action): number {
  switch (action.type) {
    case "increment":
      return count + 1;
    case "decrement":
      return count - 1;
    case "reset":
      return action.value;
    default: {
      const exhaustive: never = action;
      return exhaustive;
    }
  }
}
```

### Keep type-level programming readable

Prefer this:

```ts
type EditableUserFields = Pick<User, "email" | "name">;
type UpdateUserInput = Partial<EditableUserFields>;
```

Over this:

```ts
type UpdateUserInputHardToRead = Partial<Pick<User, "email" | "name">>;
```

### Model domain concepts, not just data shapes

```ts
type CurrencyCode = "USD" | "EUR" | "GBP";

type Money = {
  amountCents: number;
  currency: CurrencyCode;
};

function formatMoney(money: Money): string {
  return `${money.currency} ${(money.amountCents / 100).toFixed(2)}`;
}
```

Good types document intent and prevent invalid states.

### Practical checklist

- Use `strict: true` for new projects.
- Prefer inference for obvious locals; annotate boundaries.
- Use `unknown` for external data until validated.
- Prefer discriminated unions for state and events.
- Prefer `as const` plus union literals for fixed app constants.
- Prefer `satisfies` for config maps that need both validation and precise literals.
- Avoid broad assertions; narrow values instead.
- Keep generic helpers small and named.
- Use utility types for common transformations, but avoid unreadable nesting.
- Make illegal states unrepresentable whenever practical.
