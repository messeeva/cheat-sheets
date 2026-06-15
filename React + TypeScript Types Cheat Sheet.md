## 1. TypeScript Basics for React

### Primitive Types

Primitive types appear in props, state, event values, IDs, feature flags, and small helper functions.

```typescript
type UserBadgeProps = {
  name: string;
  age: number;
  isAdmin: boolean;
  deletedAt: null | string;
  nickname?: string; // string | undefined
  uniqueKey: symbol;
  largeCount: bigint;
};

function UserBadge({ name, age, isAdmin }: UserBadgeProps) {
  return <span>{isAdmin ? "Admin" : name} · {age}</span>;
}
```

Note: optional properties use `?`, which means the property may be omitted. It is usually equivalent to `property?: T`, read as `T | undefined` when accessed.

### Arrays: `string[]` vs `Array<string>`

Both are equivalent for normal arrays. Use whichever is clearer for the surrounding code.

```typescript
type TagListProps = {
  tags: string[];
  users: Array<{ id: string; name: string }>;
};

function TagList({ tags }: TagListProps) {
  return <ul>{tags.map((tag) => <li key={tag}>{tag}</li>)}</ul>;
}
```

Recommended: use `T[]` for simple arrays and `Array<T>` when the element type is complex or nested.

```typescript
type Matrix = number[][];
type QueryResult = Array<{ id: string; score: number }>;
```

### Objects and Object Shape Typing

TypeScript checks object shape, not class identity. If an object has the required properties with compatible types, it matches.

```typescript
type Product = {
  id: string;
  name: string;
  priceCents: number;
};

type ProductCardProps = {
  product: Product;
};

function ProductCard({ product }: ProductCardProps) {
  return <article>{product.name}</article>;
}
```

Pitfall: avoid overly broad object types.

```typescript
// Avoid: accepts almost any non-null object.
type BadProps = {
  product: object;
};

// Recommended: model the shape the component actually needs.
type GoodProps = {
  product: {
    id: string;
    name: string;
  };
};
```

### Optional Properties with `?`

Optional props should be handled explicitly through conditional rendering, nullish coalescing, or default values.

```typescript
type AvatarProps = {
  src?: string;
  alt: string;
  size?: number;
};

function Avatar({ src, alt, size = 40 }: AvatarProps) {
  if (!src) return <div style={{ width: size, height: size }}>{alt[0]}</div>;

  return <img src={src} alt={alt} width={size} height={size} />;
}
```

Recommended: use destructuring defaults for simple default prop values.

Avoid: making a prop optional if the component cannot render correctly without it.

### Union Types

Unions model values that can be one of several types or states.

```typescript
type Status = "idle" | "loading" | "success" | "error";

type StatusBadgeProps = {
  status: Status;
};

function StatusBadge({ status }: StatusBadgeProps) {
  return <span data-status={status}>{status}</span>;
}
```

Recommended: use string literal unions for UI states, variants, sizes, intents, and modes.

```typescript
type ButtonVariant = "primary" | "secondary" | "danger";
type ButtonSize = "sm" | "md" | "lg";
```

### Literal Types

Literal types restrict values to exact strings, numbers, or booleans.

```typescript
type ToastProps = {
  type: "success" | "error" | "info";
  durationMs?: 3000 | 5000 | 10000;
};

function Toast({ type, durationMs = 3000 }: ToastProps) {
  return <div role="status" data-type={type} data-duration={durationMs} />;
}
```

### Type Aliases

Type aliases are flexible and can represent object shapes, unions, tuples, primitives, and function types.

```typescript
type UserId = string;

type ClickHandler = (id: UserId) => void;

type UserRowProps = {
  id: UserId;
  name: string;
  onSelect: ClickHandler;
};
```

Recommended: use `type` for unions, function signatures, tuples, utility type composition, and most prop models.

### Interfaces

Interfaces are commonly used for object shapes and can be extended or merged.

```typescript
interface User {
  id: string;
  name: string;
}

interface AdminUser extends User {
  permissions: string[];
}

type AdminCardProps = {
  user: AdminUser;
};
```

Recommended: use `interface` when defining extendable object contracts, especially in shared libraries where declaration merging may be useful.

### `type` vs `interface`

| Use case | Prefer | Example |
|---|---:|---|
| Object props | Either | `type Props = { name: string }` |
| Extending object shapes | Either | `interface Admin extends User {}` |
| Union types | `type` | `type Status = "loading" \| "done"` |
| Tuple types | `type` | `type Result = [data: Data, error: Error?]` |
| Function types | `type` | `type OnSave = (id: string) => void` |
| Utility type composition | `type` | `type Props = Omit<ButtonProps, "type">` |
| Declaration merging | `interface` | `interface Window { analytics: Analytics }` |

```typescript
// type: great for unions and composition.
type AsyncState<T> =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: Error };

// interface: great for extendable object shapes.
interface BaseProps {
  id: string;
}

interface CardProps extends BaseProps {
  title: string;
}
```

Note: both `type` and `interface` are valid for component props. Consistency matters more than dogma.

### Generics

Generics let components, hooks, and helpers preserve the specific type of data they receive.

```typescript
type SelectOption<TValue extends string | number> = {
  label: string;
  value: TValue;
};

type SelectProps<TValue extends string | number> = {
  value: TValue;
  options: SelectOption<TValue>[];
  onChange: (value: TValue) => void;
};

function Select<TValue extends string | number>({
  value,
  options,
  onChange,
}: SelectProps<TValue>) {
  return (
    <select value={value} onChange={(event) => onChange(event.target.value as TValue)}>
      {options.map((option) => (
        <option key={option.value} value={option.value}>
          {option.label}
        </option>
      ))}
    </select>
  );
}
```

Pitfall: DOM form values are strings. Even if `TValue` is `number`, `event.target.value` is still a string. Parse or map values explicitly when needed.

A safer generic select can map back from the selected string to the original option value:

```typescript
type SelectProps<TValue extends string | number> = {
  value: TValue;
  options: Array<{ label: string; value: TValue }>;
  onChange: (value: TValue) => void;
};

function Select<TValue extends string | number>({ value, options, onChange }: SelectProps<TValue>) {
  return (
    <select
      value={String(value)}
      onChange={(event) => {
        const selected = options.find((option) => String(option.value) === event.target.value);
        if (selected) onChange(selected.value);
      }}
    >
      {options.map((option) => (
        <option key={String(option.value)} value={String(option.value)}>
          {option.label}
        </option>
      ))}
    </select>
  );
}
```

### Utility Types Commonly Used in React

#### `Partial<T>`

Makes all properties optional. Useful for patch updates and draft state.

```typescript
type User = {
  id: string;
  name: string;
  email: string;
};

function updateUser(id: string, patch: Partial<User>) {
  return { id, ...patch };
}
```

Pitfall: `Partial<T>` can allow incomplete values where complete values are required. Use it for patches, not full domain objects.

#### `Required<T>`

Makes all properties required. Useful after defaults are applied.

```typescript
type ModalOptions = {
  closeOnEscape?: boolean;
  closeOnBackdrop?: boolean;
};

type ResolvedModalOptions = Required<ModalOptions>;

const defaultOptions: ResolvedModalOptions = {
  closeOnEscape: true,
  closeOnBackdrop: true,
};
```

#### `Pick<T, K>`

Selects specific properties from a type.

```typescript
type User = {
  id: string;
  name: string;
  email: string;
  role: "admin" | "user";
};

type UserPreviewProps = Pick<User, "id" | "name">;

function UserPreview({ id, name }: UserPreviewProps) {
  return <span data-user-id={id}>{name}</span>;
}
```

#### `Omit<T, K>`

Removes specific properties from a type. Useful when wrapping native props or customizing external component props.

```typescript
type NativeButtonProps = React.ComponentPropsWithoutRef<"button">;

type IconButtonProps = Omit<NativeButtonProps, "children"> & {
  label: string;
  icon: React.ReactNode;
};

function IconButton({ label, icon, ...buttonProps }: IconButtonProps) {
  return (
    <button aria-label={label} {...buttonProps}>
      {icon}
    </button>
  );
}
```

#### `Record<K, T>`

Creates an object type with keys `K` and values `T`. Useful for variant maps and lookup tables.

```typescript
type ButtonVariant = "primary" | "secondary" | "danger";

const variantClassName: Record<ButtonVariant, string> = {
  primary: "btn-primary",
  secondary: "btn-secondary",
  danger: "btn-danger",
};
```

Recommended: use `Record` when every variant must have a corresponding value.

#### `Readonly<T>`

Prevents mutation of properties.

```typescript
type BreadcrumbProps = Readonly<{
  items: string[];
}>;

function Breadcrumb({ items }: BreadcrumbProps) {
  return <nav>{items.join(" / ")}</nav>;
}
```

Note: `Readonly<T>` is shallow. It does not deeply freeze nested objects or arrays.

#### `NonNullable<T>`

Removes `null` and `undefined` from a type.

```typescript
type User = {
  id: string;
  name: string;
};

type MaybeUser = User | null | undefined;
type LoadedUser = NonNullable<MaybeUser>;

function renderUser(user: MaybeUser) {
  if (!user) return null;

  const loadedUser: LoadedUser = user;
  return <span>{loadedUser.name}</span>;
}
```

#### `ReturnType<T>`

Extracts the return type of a function.

```typescript
function createInitialState() {
  return {
    status: "idle" as const,
    count: 0,
  };
}

type CounterState = ReturnType<typeof createInitialState>;

function Counter() {
  const [state] = React.useState<CounterState>(createInitialState);
  return <span>{state.count}</span>;
}
```

#### `Parameters<T>`

Extracts a function's parameter tuple.

```typescript
type SaveHandler = (id: string, value: string) => void;

type SaveArgs = Parameters<SaveHandler>; // [id: string, value: string]

function callSave(onSave: SaveHandler, ...args: SaveArgs) {
  onSave(...args);
}
```

#### `Awaited<T>`

Extracts the resolved value of a promise. Useful for API helpers.

```typescript
async function fetchUser() {
  return { id: "u1", name: "Ada" };
}

type User = Awaited<ReturnType<typeof fetchUser>>;

function UserName({ user }: { user: User }) {
  return <span>{user.name}</span>;
}
```

---

## 2. Typing React Components

### Function Components Without `React.FC`

Modern React + TypeScript does not require `React.FC`. Type props directly.

```typescript
type GreetingProps = {
  name: string;
};

function Greeting({ name }: GreetingProps) {
  return <h1>Hello, {name}</h1>;
}
```

Recommended: type the props object and let TypeScript infer the component return type unless an explicit return type clarifies the public API.

### Component with No Props

```typescript
function Spinner() {
  return <div role="status">Loading...</div>;
}
```

If you want to explicitly disallow props when assigning to a variable, use an empty object type carefully:

```typescript
type SpinnerProps = Record<string, never>;

function Spinner(_props: SpinnerProps) {
  return <div role="status">Loading...</div>;
}
```

Note: most no-prop function components do not need an explicit prop type.

### Required Props

```typescript
type ProductPriceProps = {
  amountCents: number;
  currency: "USD" | "EUR" | "GBP";
};

function ProductPrice({ amountCents, currency }: ProductPriceProps) {
  return <span>{currency} {(amountCents / 100).toFixed(2)}</span>;
}
```

### Optional Props

```typescript
type AlertProps = {
  title: string;
  description?: string;
};

function Alert({ title, description }: AlertProps) {
  return (
    <section role="alert">
      <strong>{title}</strong>
      {description && <p>{description}</p>}
    </section>
  );
}
```

Pitfall: conditional rendering with `&&` can hide valid falsy values like `0` or `""`. Use explicit checks when needed.

### Default Prop Values with Destructuring Defaults

```typescript
type BadgeProps = {
  label: string;
  tone?: "neutral" | "success" | "danger";
};

function Badge({ label, tone = "neutral" }: BadgeProps) {
  return <span data-tone={tone}>{label}</span>;
}
```

Recommended: use destructuring defaults instead of older `defaultProps` patterns for function components.

### Children Props

Children can be typed explicitly. Use `React.ReactNode` for most renderable children.

```typescript
type CardProps = {
  title: string;
  children: React.ReactNode;
};

function Card({ title, children }: CardProps) {
  return (
    <section>
      <h2>{title}</h2>
      <div>{children}</div>
    </section>
  );
}
```

Optional children:

```typescript
type EmptyStateProps = {
  title: string;
  children?: React.ReactNode;
};

function EmptyState({ title, children }: EmptyStateProps) {
  return (
    <div>
      <h2>{title}</h2>
      {children}
    </div>
  );
}
```

### `React.ReactNode`

`React.ReactNode` means anything React can render: strings, numbers, elements, fragments, portals, booleans, `null`, `undefined`, and arrays of renderable nodes.

```typescript
type StackProps = {
  children: React.ReactNode;
};

function Stack({ children }: StackProps) {
  return <div className="stack">{children}</div>;
}
```

Recommended: use `React.ReactNode` for `children`, labels, icons, descriptions, headers, footers, and slots that accept arbitrary renderable content.

### `React.ReactElement`

`React.ReactElement` means a concrete React element object, usually created by JSX. It is narrower than `ReactNode`.

```typescript
type OnlyElementProps = {
  trigger: React.ReactElement;
};

function Tooltip({ trigger }: OnlyElementProps) {
  return <span className="tooltip-trigger">{trigger}</span>;
}
```

Recommended: use `React.ReactElement` when you need a single element you may inspect, clone, or constrain.

```typescript
type CloneableTriggerProps = {
  trigger: React.ReactElement<{ disabled?: boolean }>;
};

function CloneableTrigger({ trigger }: CloneableTriggerProps) {
  return React.cloneElement(trigger, { disabled: false });
}
```

### `JSX.Element`

`JSX.Element` is the type of a JSX expression result. It is commonly used as a component return type, but it is not suitable for general children.

```typescript
function PageTitle({ title }: { title: string }): JSX.Element {
  return <h1>{title}</h1>;
}
```

Recommended: prefer inferred return types for most components. Use `JSX.Element` or `React.ReactElement | null` when an explicit component return type improves readability.

Pitfall: do not type `children` as `JSX.Element` unless the component truly requires exactly one JSX element and does not accept strings, numbers, fragments, `null`, or arrays.

### Children Type Selection

| Type | Accepts | Typical use |
|---|---|---|
| `React.ReactNode` | Anything renderable | Most `children` and visual slots |
| `React.ReactElement` | One React element object | Clone/inspect a single element |
| `JSX.Element` | JSX expression result | Explicit component return type |

### Explicit Return Type When Useful

Explicit return types are useful when a component intentionally may return `null`.

```typescript
type MaybeBannerProps = {
  visible: boolean;
  message: string;
};

function MaybeBanner({ visible, message }: MaybeBannerProps): React.ReactElement | null {
  if (!visible) return null;
  return <aside>{message}</aside>;
}
```

### Why `React.FC` Is Optional

`React.FC<Props>` is a function component helper type. It is valid, but not required.

```typescript
type LinkProps = {
  href: string;
  children: React.ReactNode;
};

const Link: React.FC<LinkProps> = ({ href, children }) => {
  return <a href={href}>{children}</a>;
};
```

Tradeoffs of `React.FC`:

| Topic | `React.FC` behavior | Practical guidance |
|---|---|---|
| Props annotation | Types the function variable | Direct function parameter typing is often simpler |
| Return type | Constrains return to React-compatible component return | Inference is usually enough |
| Children | Modern React types do not automatically add `children` the way older versions did | Type `children` explicitly either way |
| Generics | Can be awkward for generic components | Prefer plain generic functions |
| Static properties | Can be convenient in some patterns | Not a reason to use it by default |

Recommended: do not use `React.FC` as the default. Use direct props typing for simpler component declarations.

Avoid: relying on `React.FC` to communicate whether children are accepted. Make `children` explicit in props.

---

## 3. Props Patterns

### Basic Props

Props are the public API of a component. Type them at the boundary.

```typescript
type UserCardProps = {
  id: string;
  name: string;
  role: "admin" | "user";
};

function UserCard({ id, name, role }: UserCardProps) {
  return <article data-user-id={id}>{name} · {role}</article>;
}
```

Recommended: keep prop types near the component unless reused elsewhere.

### Props with Callback Functions

Callback props should describe what the component sends to the parent, not how the parent stores it.

```typescript
type UserRowProps = {
  user: { id: string; name: string };
  onSelect: (userId: string) => void;
  onRename?: (userId: string, name: string) => Promise<void> | void;
};

function UserRow({ user, onSelect, onRename }: UserRowProps) {
  return (
    <div>
      <button onClick={() => onSelect(user.id)}>{user.name}</button>
      <button onClick={() => void onRename?.(user.id, "New name")}>Rename</button>
    </div>
  );
}
```

Note: `Promise<void> | void` is useful when callers may perform async work but the component does not need the resolved value.

### Props with Union Values

```typescript
type TagProps = {
  label: string;
  color: "gray" | "blue" | "green" | "red";
};

function Tag({ label, color }: TagProps) {
  return <span data-color={color}>{label}</span>;
}
```

Recommended: use unions instead of open-ended `string` when only specific values are supported.

### Props with Discriminated Unions

Discriminated unions model mutually exclusive prop shapes.

```typescript
type AsyncContentProps<T> =
  | { status: "loading" }
  | { status: "error"; error: Error }
  | { status: "success"; data: T };

function AsyncContent<T>({ state }: { state: AsyncContentProps<T> }) {
  switch (state.status) {
    case "loading":
      return <p>Loading...</p>;
    case "error":
      return <p role="alert">{state.error.message}</p>;
    case "success":
      return <pre>{JSON.stringify(state.data, null, 2)}</pre>;
  }
}
```

Recommended: model impossible states with discriminated unions instead of loose booleans like `isLoading`, `error`, and `data` that can contradict each other.

### Props Extending Native HTML Attributes

Use native prop helpers when wrapping DOM elements.

```typescript
type ButtonProps = React.ButtonHTMLAttributes<HTMLButtonElement> & {
  variant?: "primary" | "secondary";
};

function Button({ variant = "primary", className, ...buttonProps }: ButtonProps) {
  return (
    <button
      className={["button", `button-${variant}`, className].filter(Boolean).join(" ")}
      {...buttonProps}
    />
  );
}
```

Recommended: use `ComponentPropsWithoutRef<"button">` or `ButtonHTMLAttributes<HTMLButtonElement>` for button wrappers.

### Avoiding Prop Name Conflicts When Extending Native Attributes

If your custom prop conflicts with a native prop, remove the native prop first using `Omit`.

```typescript
type CustomSize = "sm" | "md" | "lg";

type InputProps = Omit<React.ComponentPropsWithoutRef<"input">, "size"> & {
  size?: CustomSize;
};

function Input({ size = "md", ...inputProps }: InputProps) {
  return <input data-size={size} {...inputProps} />;
}
```

Pitfall: native `input` already has a numeric `size` attribute. A custom string `size` prop conflicts unless you omit the native one.

### Component Composition Props

Use `ReactNode` for slots that accept renderable content.

```typescript
type PageShellProps = {
  header: React.ReactNode;
  sidebar?: React.ReactNode;
  children: React.ReactNode;
};

function PageShell({ header, sidebar, children }: PageShellProps) {
  return (
    <div>
      <header>{header}</header>
      {sidebar && <aside>{sidebar}</aside>}
      <main>{children}</main>
    </div>
  );
}
```

### Render Props

Render props are function props that return renderable content.

```typescript
type DataLoaderProps<T> = {
  data: T[];
  children: (items: T[]) => React.ReactNode;
};

function DataLoader<T>({ data, children }: DataLoaderProps<T>) {
  return <>{children(data)}</>;
}

function Example() {
  return (
    <DataLoader data={[{ id: "1", name: "Ada" }]}>
      {(users) => users.map((user) => <div key={user.id}>{user.name}</div>)}
    </DataLoader>
  );
}
```

Recommended: name render prop functions based on intent: `children`, `renderItem`, `renderTrigger`, or `renderContent`.

### Polymorphic Components Using an `as` Prop

A polymorphic component renders different element types while preserving native props.

```typescript
type TextOwnProps<TElement extends React.ElementType> = {
  as?: TElement;
  tone?: "muted" | "strong";
  children: React.ReactNode;
};

type TextProps<TElement extends React.ElementType> = TextOwnProps<TElement> &
  Omit<React.ComponentPropsWithoutRef<TElement>, keyof TextOwnProps<TElement>>;

function Text<TElement extends React.ElementType = "span">({
  as,
  tone = "muted",
  children,
  ...props
}: TextProps<TElement>) {
  const Component = as ?? "span";

  return (
    <Component data-tone={tone} {...props}>
      {children}
    </Component>
  );
}

function Example() {
  return (
    <>
      <Text>Plain span</Text>
      <Text as="a" href="/docs">Docs link</Text>
      <Text as="button" type="button" onClick={() => console.log("clicked")}>Click</Text>
    </>
  );
}
```

Pitfall: polymorphic components are powerful but complex. Prefer simple native wrappers unless the flexibility is needed.

---

## 4. State Types

### `useState` Inference

TypeScript usually infers simple state correctly.

```typescript
function SearchBox() {
  const [query, setQuery] = React.useState("");

  return <input value={query} onChange={(event) => setQuery(event.target.value)} />;
}
```

Recommended: rely on inference for simple primitives initialized with a representative value.

### When Inference Is Enough

```typescript
const [count, setCount] = React.useState(0); // number
const [enabled, setEnabled] = React.useState(false); // boolean
const [name, setName] = React.useState(""); // string
```

### Explicit `useState` Generic Types

Use explicit generics when the initial value does not fully represent future values.

```typescript
type User = {
  id: string;
  name: string;
};

function Profile() {
  const [user, setUser] = React.useState<User | null>(null);

  if (!user) return <button onClick={() => setUser({ id: "u1", name: "Ada" })}>Load</button>;

  return <h1>{user.name}</h1>;
}
```

### Nullable State

```typescript
type User = {
  id: string;
  email: string;
};

function UserPanel() {
  const [selectedUser, setSelectedUser] = React.useState<User | null>(null);

  return selectedUser ? <p>{selectedUser.email}</p> : <p>No user selected</p>;
}
```

Recommended: use `T | null` for state that is intentionally empty before selection or loading.

Avoid: using `{} as User` as a placeholder. It bypasses safety and creates runtime risk.

### Array State

```typescript
type Todo = {
  id: string;
  text: string;
  done: boolean;
};

function TodoList() {
  const [todos, setTodos] = React.useState<Todo[]>([]);

  function addTodo(text: string) {
    setTodos((current) => [...current, { id: crypto.randomUUID(), text, done: false }]);
  }

  return <button onClick={() => addTodo("Write types")}>Add</button>;
}
```

### Avoiding `never[]`

An empty array does not tell TypeScript what element type it should contain. In some contexts, `useState([])` can infer `never[]`.

```typescript
function BadList() {
  const [items, setItems] = React.useState([]);

  // Pitfall: items may be inferred as never[], so adding an item can fail.
  // setItems([{ id: "1", label: "First" }]);

  return <div>{items.length}</div>;
}
```

Correct it with an explicit generic:

```typescript
type Item = {
  id: string;
  label: string;
};

function GoodList() {
  const [items, setItems] = React.useState<Item[]>([]);

  setItems([{ id: "1", label: "First" }]);

  return <div>{items.length}</div>;
}
```

Recommended: always type empty array state explicitly.

### Object State

```typescript
type Filters = {
  query: string;
  includeArchived: boolean;
};

function FilterPanel() {
  const [filters, setFilters] = React.useState<Filters>({
    query: "",
    includeArchived: false,
  });

  return (
    <label>
      Search
      <input
        value={filters.query}
        onChange={(event) =>
          setFilters((current) => ({ ...current, query: event.target.value }))
        }
      />
    </label>
  );
}
```

Pitfall: `useState` does not merge object state like class `setState`. Always spread the previous object when updating one field.

### Union State

Use unions for state machines and status values.

```typescript
type Status = "idle" | "saving" | "saved" | "error";

function SaveButton() {
  const [status, setStatus] = React.useState<Status>("idle");

  return (
    <button disabled={status === "saving"} onClick={() => setStatus("saving")}>
      {status === "saving" ? "Saving..." : "Save"}
    </button>
  );
}
```

### Discriminated Union State

```typescript
type User = { id: string; name: string };

type UserState =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; user: User }
  | { status: "error"; error: Error };

function UserDetails() {
  const [state, setState] = React.useState<UserState>({ status: "idle" });

  if (state.status === "success") return <h1>{state.user.name}</h1>;
  if (state.status === "error") return <p>{state.error.message}</p>;

  return <button onClick={() => setState({ status: "loading" })}>Load</button>;
}
```

Recommended: use discriminated unions when different states require different fields.

### Functional State Updates

Use functional updates when the next state depends on the previous state.

```typescript
function Counter() {
  const [count, setCount] = React.useState(0);

  return <button onClick={() => setCount((current) => current + 1)}>{count}</button>;
}
```

Recommended: use functional updates for counters, toggles, array updates, object patches, and async event handlers that may close over stale values.

---

## 5. Event Types

React wraps browser events in React event types. Inline handlers are inferred automatically; named handlers usually need annotations.

### Inline Handler Inference

```typescript
function SearchInput() {
  return (
    <input
      onChange={(event) => {
        // event is inferred as React.ChangeEvent<HTMLInputElement>
        console.log(event.target.value);
      }}
    />
  );
}
```

Recommended: write handlers inline first to inspect inferred types, then extract named handlers with the same type.

### Button Click Events

```typescript
function SaveButton() {
  function handleClick(event: React.MouseEvent<HTMLButtonElement>) {
    event.currentTarget.disabled = true;
  }

  return <button onClick={handleClick}>Save</button>;
}
```

Note: prefer `event.currentTarget` over `event.target` when accessing the element the handler is attached to.

### Input Change Events

```typescript
function NameField() {
  const [name, setName] = React.useState("");

  function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
    setName(event.currentTarget.value);
  }

  return <input value={name} onChange={handleChange} />;
}
```

### Textarea Change Events

```typescript
function BioField() {
  const [bio, setBio] = React.useState("");

  function handleChange(event: React.ChangeEvent<HTMLTextAreaElement>) {
    setBio(event.currentTarget.value);
  }

  return <textarea value={bio} onChange={handleChange} />;
}
```

### Select Change Events

```typescript
function RoleSelect() {
  const [role, setRole] = React.useState<"admin" | "user">("user");

  function handleChange(event: React.ChangeEvent<HTMLSelectElement>) {
    const value = event.currentTarget.value;
    if (value === "admin" || value === "user") setRole(value);
  }

  return (
    <select value={role} onChange={handleChange}>
      <option value="user">User</option>
      <option value="admin">Admin</option>
    </select>
  );
}
```

Pitfall: select values are strings. Narrow before setting literal-union state.

### Form Submit Events

```typescript
function LoginForm() {
  function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
    event.preventDefault();
    const formData = new FormData(event.currentTarget);
    const email = String(formData.get("email") ?? "");
    console.log(email);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input name="email" type="email" />
      <button type="submit">Log in</button>
    </form>
  );
}
```

### Keyboard Events

```typescript
function CommandInput() {
  function handleKeyDown(event: React.KeyboardEvent<HTMLInputElement>) {
    if (event.key === "Enter") {
      console.log(event.currentTarget.value);
    }
  }

  return <input onKeyDown={handleKeyDown} />;
}
```

### Mouse Events

```typescript
function HoverCard() {
  function handleMouseEnter(event: React.MouseEvent<HTMLDivElement>) {
    console.log(event.currentTarget.dataset.cardId);
  }

  return <div data-card-id="card-1" onMouseEnter={handleMouseEnter}>Hover me</div>;
}
```

### Focus and Blur Events

```typescript
function EmailInput() {
  function handleBlur(event: React.FocusEvent<HTMLInputElement>) {
    if (!event.currentTarget.value.includes("@")) {
      console.log("Invalid email");
    }
  }

  return <input type="email" onBlur={handleBlur} />;
}
```

### Drag Events

```typescript
function DropZone() {
  function handleDrop(event: React.DragEvent<HTMLDivElement>) {
    event.preventDefault();
    const files = Array.from(event.dataTransfer.files);
    console.log(files);
  }

  return <div onDragOver={(event) => event.preventDefault()} onDrop={handleDrop}>Drop files</div>;
}
```

### Clipboard Events

```typescript
function PasteInput() {
  function handlePaste(event: React.ClipboardEvent<HTMLInputElement>) {
    const text = event.clipboardData.getData("text");
    console.log(text);
  }

  return <input onPaste={handlePaste} />;
}
```

### Generic Event Typing Patterns

```typescript
function preventDefault<TElement extends HTMLElement>(
  handler: (event: React.SyntheticEvent<TElement>) => void,
) {
  return (event: React.SyntheticEvent<TElement>) => {
    event.preventDefault();
    handler(event);
  };
}
```

Use specific event types when you need event-specific fields like `clipboardData`, `dataTransfer`, or `key`.

### Event Object Types vs Handler Helper Types

Handler helper types type the whole function instead of the event parameter.

```typescript
const handleInputChange: React.ChangeEventHandler<HTMLInputElement> = (event) => {
  console.log(event.currentTarget.value);
};

const handleButtonClick: React.MouseEventHandler<HTMLButtonElement> = (event) => {
  console.log(event.currentTarget.name);
};
```

Recommended:

```typescript
function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
  console.log(event.currentTarget.value);
}
```

Also recommended when passing handlers as props:

```typescript
type SearchProps = {
  onChange: React.ChangeEventHandler<HTMLInputElement>;
};

function Search({ onChange }: SearchProps) {
  return <input onChange={onChange} />;
}
```

---

## 6. Refs

### `useRef` with DOM Elements

DOM refs are usually nullable because React sets them after render and clears them on unmount.

```typescript
function FocusInput() {
  const inputRef = React.useRef<HTMLInputElement | null>(null);

  function focusInput() {
    inputRef.current?.focus();
  }

  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus</button>
    </>
  );
}
```

Recommended: initialize DOM refs with `null` and include `| null` in the type.

Avoid: `useRef<HTMLInputElement>(null!)` unless you have a narrow, justified reason and can guarantee the ref exists before access.

### Mutable Refs for Values That Do Not Trigger Re-renders

Use refs for mutable values that should persist across renders without causing re-renders.

```typescript
function Stopwatch() {
  const startTimeRef = React.useRef<number | null>(null);

  function start() {
    startTimeRef.current = Date.now();
  }

  function stop() {
    if (startTimeRef.current !== null) {
      console.log(Date.now() - startTimeRef.current);
    }
  }

  return (
    <>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
    </>
  );
}
```

### Timer Ref

Browser timers and Node timers can differ depending on project configuration. `ReturnType<typeof setTimeout>` is portable.

```typescript
function DelayedMessage() {
  const timeoutRef = React.useRef<ReturnType<typeof setTimeout> | null>(null);

  React.useEffect(() => {
    timeoutRef.current = setTimeout(() => console.log("Done"), 1000);

    return () => {
      if (timeoutRef.current) clearTimeout(timeoutRef.current);
    };
  }, []);

  return null;
}
```

### Forwarding Refs with `React.forwardRef`

Use `forwardRef` when a parent needs access to a child component's DOM node or imperative API.

```typescript
type TextInputProps = React.ComponentPropsWithoutRef<"input"> & {
  label: string;
};

const TextInput = React.forwardRef<HTMLInputElement, TextInputProps>(
  ({ label, ...inputProps }, ref) => {
    return (
      <label>
        {label}
        <input ref={ref} {...inputProps} />
      </label>
    );
  },
);

TextInput.displayName = "TextInput";
```

Recommended: provide both the ref element type and prop type to `forwardRef<RefType, PropsType>`.

### `useImperativeHandle`

Expose a limited imperative API instead of the entire DOM node.

```typescript
type SearchInputHandle = {
  focus: () => void;
  clear: () => void;
};

type SearchInputProps = {
  initialValue?: string;
};

const SearchInput = React.forwardRef<SearchInputHandle, SearchInputProps>(
  ({ initialValue = "" }, ref) => {
    const [value, setValue] = React.useState(initialValue);
    const inputRef = React.useRef<HTMLInputElement | null>(null);

    React.useImperativeHandle(ref, () => ({
      focus: () => inputRef.current?.focus(),
      clear: () => setValue(""),
    }));

    return <input ref={inputRef} value={value} onChange={(event) => setValue(event.target.value)} />;
  },
);

SearchInput.displayName = "SearchInput";
```

Recommended: keep imperative handles small and stable.

### Typing Component Refs

Use `React.ElementRef<typeof Component>` to extract the ref type from a component or intrinsic element.

```typescript
type ButtonRef = React.ElementRef<"button">; // HTMLButtonElement

type InputRef = React.ElementRef<typeof TextInput>; // HTMLInputElement

function Parent() {
  const inputRef = React.useRef<InputRef | null>(null);

  return <TextInput ref={inputRef} label="Name" />;
}
```

Note: `ElementRef` only works when the component supports refs, such as intrinsic elements or components created with `forwardRef`.

---

## 7. Forms

### Controlled Inputs

Controlled inputs store form values in React state. This gives strong typing at the state boundary.

```typescript
type LoginValues = {
  email: string;
  password: string;
};

function LoginForm() {
  const [values, setValues] = React.useState<LoginValues>({
    email: "",
    password: "",
  });

  function updateField(field: keyof LoginValues, value: string) {
    setValues((current) => ({ ...current, [field]: value }));
  }

  return (
    <form>
      <input
        value={values.email}
        onChange={(event) => updateField("email", event.currentTarget.value)}
      />
      <input
        type="password"
        value={values.password}
        onChange={(event) => updateField("password", event.currentTarget.value)}
      />
    </form>
  );
}
```

Recommended: controlled state is useful when values affect rendering, validation, autosave, or interdependent fields.

### Uncontrolled Forms with `FormData`

Uncontrolled forms read values on submit.

```typescript
type SignupValues = {
  email: string;
  displayName: string;
};

function SignupForm() {
  function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
    event.preventDefault();

    const formData = new FormData(event.currentTarget);
    const values: SignupValues = {
      email: String(formData.get("email") ?? ""),
      displayName: String(formData.get("displayName") ?? ""),
    };

    console.log(values);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input name="email" type="email" />
      <input name="displayName" />
      <button type="submit">Create account</button>
    </form>
  );
}
```

Note: `FormData.get()` returns `FormDataEntryValue | null`, where `FormDataEntryValue` is `string | File`. Narrow or convert before assigning to typed values.

### Safely Reading Values from Form Elements

For small forms, typed `elements` access can be useful.

```typescript
type LoginFormElements = HTMLFormControlsCollection & {
  email: HTMLInputElement;
  password: HTMLInputElement;
};

type LoginFormElement = HTMLFormElement & {
  readonly elements: LoginFormElements;
};

function LoginForm() {
  function handleSubmit(event: React.FormEvent<LoginFormElement>) {
    event.preventDefault();

    const form = event.currentTarget;
    const email = form.elements.email.value;
    const password = form.elements.password.value;

    console.log({ email, password });
  }

  return (
    <form onSubmit={handleSubmit}>
      <input name="email" type="email" />
      <input name="password" type="password" />
      <button type="submit">Log in</button>
    </form>
  );
}
```

Pitfall: this type must match the actual `name` attributes. Rename fields carefully.

### Reusable Input Components

Extend native input props to preserve expected attributes like `value`, `onChange`, `name`, `type`, and `disabled`.

```typescript
type TextFieldProps = Omit<React.InputHTMLAttributes<HTMLInputElement>, "size"> & {
  label: string;
  size?: "sm" | "md" | "lg";
};

function TextField({ label, size = "md", id, ...inputProps }: TextFieldProps) {
  const generatedId = React.useId();
  const inputId = id ?? generatedId;

  return (
    <label htmlFor={inputId} data-size={size}>
      {label}
      <input id={inputId} {...inputProps} />
    </label>
  );
}
```

Recommended: use `Omit` to resolve conflicts with native props.

### Custom Submit Handler with Typed Values

```typescript
type ContactValues = {
  email: string;
  message: string;
};

type ContactFormProps = {
  onSubmit: (values: ContactValues) => void | Promise<void>;
};

function ContactForm({ onSubmit }: ContactFormProps) {
  const [values, setValues] = React.useState<ContactValues>({ email: "", message: "" });

  function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
    event.preventDefault();
    void onSubmit(values);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={values.email}
        onChange={(event) => setValues((current) => ({ ...current, email: event.target.value }))}
      />
      <textarea
        value={values.message}
        onChange={(event) => setValues((current) => ({ ...current, message: event.target.value }))}
      />
      <button type="submit">Send</button>
    </form>
  );
}
```

### Typed State vs `FormData`

| Approach | Best for | Tradeoff |
|---|---|---|
| Typed React state | Dynamic UI, live validation, controlled fields | More boilerplate |
| `FormData` | Simple submit-only forms, native forms | Values require conversion/narrowing |
| Typed `elements` | Small forms with stable field names | Manual type must match markup |

---

## 8. Context

### Creating Typed Context with a Real Default Value

Use a real default when the fallback is meaningful outside a provider.

```typescript
type Theme = "light" | "dark";

type ThemeContextValue = {
  theme: Theme;
  setTheme: (theme: Theme) => void;
};

const ThemeContext = React.createContext<ThemeContextValue>({
  theme: "light",
  setTheme: () => undefined,
});
```

Note: a no-op default setter is acceptable only when using the context outside a provider is valid or intentionally harmless.

### Context Initialized with `null`

Use `null` when there is no safe default value.

```typescript
type AuthUser = {
  id: string;
  name: string;
};

type AuthContextValue = {
  user: AuthUser;
  logout: () => void;
};

const AuthContext = React.createContext<AuthContextValue | null>(null);
```

### Custom Context Hook That Throws Outside Provider

```typescript
function useAuth() {
  const context = React.useContext(AuthContext);

  if (context === null) {
    throw new Error("useAuth must be used within an AuthProvider");
  }

  return context;
}

function UserMenu() {
  const { user, logout } = useAuth();

  return <button onClick={logout}>{user.name}</button>;
}
```

Recommended: use a custom hook to narrow `null` once and keep consuming components clean.

### Provider Example

```typescript
type AuthProviderProps = {
  user: AuthUser;
  children: React.ReactNode;
};

function AuthProvider({ user, children }: AuthProviderProps) {
  const value = React.useMemo<AuthContextValue>(
    () => ({
      user,
      logout: () => console.log("logout"),
    }),
    [user],
  );

  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}
```

### Context with Reducers

```typescript
type CounterState = { count: number };

type CounterAction =
  | { type: "increment" }
  | { type: "decrement" }
  | { type: "reset"; value?: number };

type CounterContextValue = {
  state: CounterState;
  dispatch: React.Dispatch<CounterAction>;
};

const CounterContext = React.createContext<CounterContextValue | null>(null);

function counterReducer(state: CounterState, action: CounterAction): CounterState {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return { count: action.value ?? 0 };
  }
}

function CounterProvider({ children }: { children: React.ReactNode }) {
  const [state, dispatch] = React.useReducer(counterReducer, { count: 0 });

  return (
    <CounterContext.Provider value={{ state, dispatch }}>
      {children}
    </CounterContext.Provider>
  );
}
```

### Avoid Unsafe Placeholder Defaults

```typescript
// Avoid: hides missing provider errors and can crash later.
const UnsafeAuthContext = React.createContext<AuthContextValue>({} as AuthContextValue);
```

Correct pattern:

```typescript
const SafeAuthContext = React.createContext<AuthContextValue | null>(null);

function useSafeAuth() {
  const context = React.useContext(SafeAuthContext);
  if (!context) throw new Error("useSafeAuth must be used within SafeAuthContext.Provider");
  return context;
}
```

Recommended: prefer `T | null` plus a custom hook when no real default exists.

---

## 9. Reducers

Reducers benefit from explicit state and action types because they centralize state transitions.

### Counter Reducer

```typescript
type CounterState = {
  count: number;
};

type CounterAction =
  | { type: "increment" }
  | { type: "decrement" }
  | { type: "set"; value: number };

function counterReducer(state: CounterState, action: CounterAction): CounterState {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "set":
      return { count: action.value };
  }
}

function Counter() {
  const [state, dispatch] = React.useReducer(counterReducer, { count: 0 });

  return (
    <button onClick={() => dispatch({ type: "increment" })}>
      {state.count}
    </button>
  );
}
```

Action unions improve autocomplete: after typing `dispatch({ type: "set", ... })`, TypeScript knows `value` is required.

### Exhaustiveness Checking with `never`

```typescript
function assertNever(value: never): never {
  throw new Error(`Unexpected value: ${JSON.stringify(value)}`);
}

type StatusAction =
  | { type: "start" }
  | { type: "succeed"; data: string[] }
  | { type: "fail"; error: Error };

type StatusState =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; error: Error };

function statusReducer(state: StatusState, action: StatusAction): StatusState {
  switch (action.type) {
    case "start":
      return { status: "loading" };
    case "succeed":
      return { status: "success", data: action.data };
    case "fail":
      return { status: "error", error: action.error };
    default:
      return assertNever(action);
  }
}
```

Recommended: use `assertNever` in reducers with action unions that are likely to grow.

### Todo Reducer

```typescript
type Todo = {
  id: string;
  text: string;
  done: boolean;
};

type TodoState = {
  todos: Todo[];
};

type TodoAction =
  | { type: "add"; text: string }
  | { type: "toggle"; id: string }
  | { type: "remove"; id: string };

function todoReducer(state: TodoState, action: TodoAction): TodoState {
  switch (action.type) {
    case "add":
      return {
        todos: [...state.todos, { id: crypto.randomUUID(), text: action.text, done: false }],
      };
    case "toggle":
      return {
        todos: state.todos.map((todo) =>
          todo.id === action.id ? { ...todo, done: !todo.done } : todo,
        ),
      };
    case "remove":
      return {
        todos: state.todos.filter((todo) => todo.id !== action.id),
      };
  }
}
```

### Typing Reducer Dispatch

```typescript
type TodoDispatch = React.Dispatch<TodoAction>;

type TodoToolbarProps = {
  dispatch: TodoDispatch;
};

function TodoToolbar({ dispatch }: TodoToolbarProps) {
  return <button onClick={() => dispatch({ type: "add", text: "New todo" })}>Add</button>;
}
```

Recommended: export `State`, `Action`, and possibly `Dispatch` types when a reducer is shared through context.

---

## 10. Custom Hooks

### Typing Hook Parameters

```typescript
type UseToggleOptions = {
  initialValue?: boolean;
};

function useToggle({ initialValue = false }: UseToggleOptions = {}) {
  const [value, setValue] = React.useState(initialValue);
  const toggle = React.useCallback(() => setValue((current) => !current), []);

  return { value, setValue, toggle };
}
```

### Hook Returning an Object

Object returns are self-documenting and flexible.

```typescript
type UseDisclosureReturn = {
  isOpen: boolean;
  open: () => void;
  close: () => void;
  toggle: () => void;
};

function useDisclosure(initialValue = false): UseDisclosureReturn {
  const [isOpen, setIsOpen] = React.useState(initialValue);

  return {
    isOpen,
    open: () => setIsOpen(true),
    close: () => setIsOpen(false),
    toggle: () => setIsOpen((current) => !current),
  };
}
```

Recommended: use object returns for hooks with more than two values or when names matter.

### Hook Returning a Tuple

Tuples are useful when callers can name the returned values themselves, similar to `useState`.

```typescript
function useBoolean(initialValue = false): readonly [boolean, () => void, () => void] {
  const [value, setValue] = React.useState(initialValue);

  const setTrue = React.useCallback(() => setValue(true), []);
  const setFalse = React.useCallback(() => setValue(false), []);

  return [value, setTrue, setFalse] as const;
}
```

Use `as const` to preserve tuple positions instead of widening to an array of mixed types.

```typescript
function useCounter(initialValue = 0) {
  const [count, setCount] = React.useState(initialValue);
  const increment = () => setCount((current) => current + 1);

  return [count, increment] as const;
}
```

Pitfall: without `as const` or an explicit tuple return type, TypeScript may infer `(number | (() => void))[]`.

### Generic `useLocalStorage`-Style Hook

```typescript
function useLocalStorage<T>(key: string, initialValue: T) {
  const [value, setValue] = React.useState<T>(() => {
    const raw = window.localStorage.getItem(key);
    if (raw === null) return initialValue;
    return JSON.parse(raw) as T;
  });

  React.useEffect(() => {
    window.localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue] as const;
}
```

Pitfall: `JSON.parse` returns `any`. Treat persistence and network boundaries as unsafe. For production-grade code, validate parsed data before trusting it.

Safer shape with a parser:

```typescript
function useParsedLocalStorage<T>(
  key: string,
  initialValue: T,
  parse: (value: unknown) => T,
) {
  const [value, setValue] = React.useState<T>(() => {
    const raw = window.localStorage.getItem(key);
    if (raw === null) return initialValue;

    try {
      return parse(JSON.parse(raw) as unknown);
    } catch {
      return initialValue;
    }
  });

  React.useEffect(() => {
    window.localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue] as const;
}
```

### Hook Accepting a Callback

```typescript
function useWindowEvent<K extends keyof WindowEventMap>(
  type: K,
  handler: (event: WindowEventMap[K]) => void,
) {
  React.useEffect(() => {
    window.addEventListener(type, handler);
    return () => window.removeEventListener(type, handler);
  }, [type, handler]);
}
```

Usage:

```typescript
function Example() {
  useWindowEvent("resize", (event) => {
    console.log(event.type);
  });

  return null;
}
```

### Hook Returning a DOM Ref

```typescript
function useAutoFocus<TElement extends HTMLElement>() {
  const ref = React.useRef<TElement | null>(null);

  React.useEffect(() => {
    ref.current?.focus();
  }, []);

  return ref;
}

function Example() {
  const inputRef = useAutoFocus<HTMLInputElement>();
  return <input ref={inputRef} />;
}
```

### Explicit Return Types for Hook APIs

Explicit return types make reusable hooks easier to consume and harder to accidentally break.

```typescript
type UseAsyncReturn<T> = {
  data: T | null;
  error: Error | null;
  isLoading: boolean;
};

function useAsyncValue<T>(load: () => Promise<T>): UseAsyncReturn<T> {
  const [data, setData] = React.useState<T | null>(null);
  const [error, setError] = React.useState<Error | null>(null);
  const [isLoading, setIsLoading] = React.useState(false);

  React.useEffect(() => {
    setIsLoading(true);
    load()
      .then(setData)
      .catch((reason: unknown) => {
        setError(reason instanceof Error ? reason : new Error("Unknown error"));
      })
      .finally(() => setIsLoading(false));
  }, [load]);

  return { data, error, isLoading };
}
```

---

## 11. Async Types

### Typing Promises

```typescript
type User = {
  id: string;
  name: string;
};

async function getUser(id: string): Promise<User> {
  const response = await fetch(`/api/users/${id}`);
  const data = (await response.json()) as unknown;

  if (isUser(data)) return data;
  throw new Error("Invalid user response");
}

function isUser(value: unknown): value is User {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "name" in value &&
    typeof value.id === "string" &&
    typeof value.name === "string"
  );
}
```

Recommended: annotate exported async functions with `Promise<T>`.

### Async Functions in Components

Do not make the component function itself `async`. Put async logic in event handlers, effects, or framework-specific data APIs.

```typescript
function SaveProfileButton({ userId }: { userId: string }) {
  const [isSaving, setIsSaving] = React.useState(false);

  async function handleClick() {
    setIsSaving(true);
    try {
      await fetch(`/api/users/${userId}`, { method: "PATCH" });
    } finally {
      setIsSaving(false);
    }
  }

  return <button disabled={isSaving} onClick={() => void handleClick()}>Save</button>;
}
```

Note: `void handleClick()` communicates that the returned promise is intentionally not awaited by React's event system.

### Fetch Response Typing

`response.json()` is a type boundary. TypeScript cannot know the runtime shape of JSON.

```typescript
async function fetchJson<T>(url: string, validate: (value: unknown) => value is T): Promise<T> {
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error(`Request failed: ${response.status}`);
  }

  const value = (await response.json()) as unknown;

  if (!validate(value)) {
    throw new Error("Invalid response shape");
  }

  return value;
}
```

Avoid:

```typescript
async function unsafeFetchUser(): Promise<User> {
  const response = await fetch("/api/user");
  return response.json(); // Avoid: trusts unknown JSON as User.
}
```

### Loading/Error/Data State

Use a discriminated union to prevent impossible combinations.

```typescript
type AsyncState<T> =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: Error };

function UserPanel() {
  const [state, setState] = React.useState<AsyncState<User>>({ status: "idle" });

  async function loadUser() {
    setState({ status: "loading" });

    try {
      const user = await getUser("u1");
      setState({ status: "success", data: user });
    } catch (reason: unknown) {
      setState({
        status: "error",
        error: reason instanceof Error ? reason : new Error("Unknown error"),
      });
    }
  }

  if (state.status === "success") return <p>{state.data.name}</p>;
  if (state.status === "error") return <p>{state.error.message}</p>;

  return <button onClick={() => void loadUser()}>Load</button>;
}
```

### Generic `useFetch<T>` Pattern

```typescript
type FetchState<T> =
  | { status: "idle" | "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: Error };

function useFetch<T>(url: string, validate: (value: unknown) => value is T) {
  const [state, setState] = React.useState<FetchState<T>>({ status: "idle" });

  React.useEffect(() => {
    const controller = new AbortController();

    async function load() {
      setState({ status: "loading" });

      try {
        const response = await fetch(url, { signal: controller.signal });
        const value = (await response.json()) as unknown;

        if (!validate(value)) throw new Error("Invalid response shape");

        setState({ status: "success", data: value });
      } catch (reason: unknown) {
        if (reason instanceof DOMException && reason.name === "AbortError") return;
        setState({
          status: "error",
          error: reason instanceof Error ? reason : new Error("Unknown error"),
        });
      }
    }

    void load();

    return () => controller.abort();
  }, [url, validate]);

  return state;
}
```

Recommended: accept a validator/parser for generic fetch hooks. A generic type parameter alone does not validate runtime data.

### Safe Error Handling with `unknown`

```typescript
function toError(reason: unknown): Error {
  if (reason instanceof Error) return reason;
  if (typeof reason === "string") return new Error(reason);
  return new Error("Unknown error");
}

async function saveSettings() {
  try {
    await fetch("/api/settings", { method: "POST" });
  } catch (reason: unknown) {
    console.error(toError(reason).message);
  }
}
```

Recommended: use `unknown` for caught errors before narrowing.

Avoid: `catch (error: any)`.

---

## 12. Component Props Helpers

React ships many helper types for extracting and composing props.

### `ComponentProps`

Gets the props for an intrinsic element or component, including ref handling where applicable.

```typescript
type ButtonProps = React.ComponentProps<"button">;

function NativeButton(props: ButtonProps) {
  return <button {...props} />;
}
```

Use when: you want the full prop type of an element or component.

### `ComponentPropsWithoutRef`

Gets props without `ref`. Best default for DOM wrapper components that do not forward refs.

```typescript
type ButtonProps = React.ComponentPropsWithoutRef<"button"> & {
  variant?: "primary" | "secondary";
};

function Button({ variant = "primary", ...props }: ButtonProps) {
  return <button data-variant={variant} {...props} />;
}
```

Use when: wrapping an element and not forwarding refs.

### `ComponentPropsWithRef`

Gets props including `ref`. Useful when forwarding refs or mirroring another component.

```typescript
type InputProps = React.ComponentPropsWithRef<"input">;

const Input = React.forwardRef<HTMLInputElement, InputProps>((props, ref) => {
  return <input ref={ref} {...props} />;
});

Input.displayName = "Input";
```

Use when: the component accepts and forwards a `ref`.

### `ElementRef`

Extracts the instance/ref type for an element or ref-forwarding component.

```typescript
type InputElement = React.ElementRef<"input">; // HTMLInputElement

const inputRef = React.createRef<InputElement>();
```

Use when: you need the ref target type of an intrinsic element or forwarded-ref component.

### `PropsWithChildren`

Adds optional `children?: ReactNode` to a prop type.

```typescript
type PanelProps = React.PropsWithChildren<{
  title: string;
}>;

function Panel({ title, children }: PanelProps) {
  return <section><h2>{title}</h2>{children}</section>;
}
```

Use when: children are optional and you want a concise helper.

Recommended: explicitly type `children` yourself when children are required.

```typescript
type RequiredChildrenPanelProps = {
  title: string;
  children: React.ReactNode;
};
```

### `HTMLAttributes`

Generic attributes for many HTML elements, but not element-specific attributes like button `type` or input `value` details.

```typescript
type BoxProps = React.HTMLAttributes<HTMLDivElement> & {
  padded?: boolean;
};

function Box({ padded, ...props }: BoxProps) {
  return <div data-padded={padded} {...props} />;
}
```

Use when: wrapping generic elements like `div` or `span`.

Avoid: using `HTMLAttributes` for `button`, `input`, or `a` when specific helpers are available.

### `ButtonHTMLAttributes`

```typescript
type SubmitButtonProps = React.ButtonHTMLAttributes<HTMLButtonElement> & {
  isLoading?: boolean;
};

function SubmitButton({ isLoading, disabled, ...props }: SubmitButtonProps) {
  return <button disabled={disabled || isLoading} {...props} />;
}
```

Use when: wrapping a `button` and preserving button-specific props.

### `InputHTMLAttributes`

```typescript
type CheckboxProps = Omit<React.InputHTMLAttributes<HTMLInputElement>, "type"> & {
  label: string;
};

function Checkbox({ label, ...props }: CheckboxProps) {
  return <label><input type="checkbox" {...props} /> {label}</label>;
}
```

Use when: wrapping an `input` and preserving input-specific props.

### `AnchorHTMLAttributes`

```typescript
type ExternalLinkProps = React.AnchorHTMLAttributes<HTMLAnchorElement> & {
  href: string;
};

function ExternalLink({ href, children, ...props }: ExternalLinkProps) {
  return <a href={href} target="_blank" rel="noreferrer" {...props}>{children}</a>;
}
```

Use when: wrapping an anchor.

### `ChangeEventHandler`

Types a complete change handler function.

```typescript
type SearchProps = {
  onChange: React.ChangeEventHandler<HTMLInputElement>;
};

function Search({ onChange }: SearchProps) {
  return <input type="search" onChange={onChange} />;
}
```

Use when: accepting or storing handler functions.

### `MouseEventHandler`

```typescript
type ClickableProps = {
  onClick?: React.MouseEventHandler<HTMLButtonElement>;
};

function Clickable({ onClick }: ClickableProps) {
  return <button onClick={onClick}>Click</button>;
}
```

Use when: accepting click handlers as props.

### `Dispatch`

Represents a reducer or state dispatch function.

```typescript
type Action = { type: "open" } | { type: "close" };

type ToolbarProps = {
  dispatch: React.Dispatch<Action>;
};
```

Use when: passing reducer dispatch down to children or context.

### `SetStateAction`

Represents either a direct state value or an updater function.

```typescript
type TextInputProps = {
  value: string;
  setValue: React.Dispatch<React.SetStateAction<string>>;
};

function TextInput({ value, setValue }: TextInputProps) {
  return <input value={value} onChange={(event) => setValue(event.target.value)} />;
}
```

Use when: passing a state setter itself.

Recommended: for reusable components, prefer intention-specific callbacks like `onValueChange(value: string)` instead of exposing raw setters unless the child truly needs setter semantics.

---

## 13. DOM and HTML Attribute Types

### Extending Native Element Props

Preserve native props with `ComponentPropsWithoutRef` when wrapping DOM elements.

```typescript
type ContainerProps = React.ComponentPropsWithoutRef<"div"> & {
  maxWidth?: "sm" | "md" | "lg";
};

function Container({ maxWidth = "md", ...divProps }: ContainerProps) {
  return <div data-max-width={maxWidth} {...divProps} />;
}
```

### Typing Buttons

```typescript
type ButtonProps = React.ComponentPropsWithoutRef<"button"> & {
  variant?: "primary" | "danger";
};

function Button({ variant = "primary", type = "button", ...props }: ButtonProps) {
  return <button type={type} data-variant={variant} {...props} />;
}
```

Recommended: default custom buttons to `type="button"` unless they are specifically submit buttons.

### Typing Inputs

```typescript
type InputProps = Omit<React.ComponentPropsWithoutRef<"input">, "size"> & {
  label: string;
  size?: "sm" | "md" | "lg";
};

function Input({ label, size = "md", id, ...props }: InputProps) {
  const generatedId = React.useId();
  const inputId = id ?? generatedId;

  return (
    <label htmlFor={inputId}>
      {label}
      <input id={inputId} data-size={size} {...props} />
    </label>
  );
}
```

### Typing Links

```typescript
type LinkProps = React.ComponentPropsWithoutRef<"a"> & {
  external?: boolean;
};

function Link({ external = false, target, rel, ...props }: LinkProps) {
  return (
    <a
      target={external ? "_blank" : target}
      rel={external ? "noreferrer" : rel}
      {...props}
    />
  );
}
```

### Typing Divs and Spans

```typescript
type BoxProps = React.ComponentPropsWithoutRef<"div"> & {
  visuallyHidden?: boolean;
};

function Box({ visuallyHidden, ...props }: BoxProps) {
  return <div data-visually-hidden={visuallyHidden} {...props} />;
}

type TextProps = React.ComponentPropsWithoutRef<"span"> & {
  tone?: "muted" | "normal";
};

function Text({ tone = "normal", ...props }: TextProps) {
  return <span data-tone={tone} {...props} />;
}
```

### Passing Through Native Props with Rest/Spread

```typescript
type IconButtonProps = Omit<React.ComponentPropsWithoutRef<"button">, "children"> & {
  icon: React.ReactNode;
  label: string;
};

function IconButton({ icon, label, ...buttonProps }: IconButtonProps) {
  return (
    <button aria-label={label} {...buttonProps}>
      {icon}
    </button>
  );
}
```

Recommended: destructure custom props first, then spread native props onto the correct element.

Pitfall: spread order matters. Later props override earlier props.

### Choosing Between `HTMLAttributes`, Specific Attributes, and `ComponentPropsWithoutRef`

| Need | Prefer | Why |
|---|---|---|
| Generic `div` or `span` wrapper | `ComponentPropsWithoutRef<"div">` or `HTMLAttributes<HTMLDivElement>` | Includes generic DOM props |
| Button wrapper | `ComponentPropsWithoutRef<"button">` or `ButtonHTMLAttributes<HTMLButtonElement>` | Includes button-specific props |
| Input wrapper | `ComponentPropsWithoutRef<"input">` or `InputHTMLAttributes<HTMLInputElement>` | Includes input-specific props |
| Link wrapper | `ComponentPropsWithoutRef<"a">` or `AnchorHTMLAttributes<HTMLAnchorElement>` | Includes anchor-specific props |
| Mirror another component | `ComponentPropsWithoutRef<typeof Component>` | Tracks source component props |

Recommended: `ComponentPropsWithoutRef<"element">` is a strong default for wrappers because it matches JSX intrinsic element props closely.

---

## 14. Advanced Patterns

### Generic Components

Generic components preserve item-specific types.

```typescript
type ListProps<T> = {
  items: T[];
  getKey: (item: T) => React.Key;
  renderItem: (item: T) => React.ReactNode;
};

function List<T>({ items, getKey, renderItem }: ListProps<T>) {
  return <ul>{items.map((item) => <li key={getKey(item)}>{renderItem(item)}</li>)}</ul>;
}

function Example() {
  return (
    <List
      items={[{ id: "u1", name: "Ada" }]}
      getKey={(user) => user.id}
      renderItem={(user) => user.name}
    />
  );
}
```

Recommended: use generics when the component should work with many data shapes while preserving exact item types.

### Generic Table Component with Typed Columns

```typescript
type Column<T> = {
  key: string;
  header: React.ReactNode;
  render: (row: T) => React.ReactNode;
};

type TableProps<T> = {
  rows: T[];
  columns: Column<T>[];
  getRowKey: (row: T) => React.Key;
};

function Table<T>({ rows, columns, getRowKey }: TableProps<T>) {
  return (
    <table>
      <thead>
        <tr>{columns.map((column) => <th key={column.key}>{column.header}</th>)}</tr>
      </thead>
      <tbody>
        {rows.map((row) => (
          <tr key={getRowKey(row)}>
            {columns.map((column) => <td key={column.key}>{column.render(row)}</td>)}
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```

Usage:

```typescript
type User = {
  id: string;
  name: string;
  email: string;
};

const userColumns: Column<User>[] = [
  { key: "name", header: "Name", render: (user) => user.name },
  { key: "email", header: "Email", render: (user) => <a href={`mailto:${user.email}`}>{user.email}</a> },
];
```

### Conditional Props

Use unions when one prop controls whether another prop is required.

```typescript
type DialogProps =
  | { controlled: true; open: boolean; onOpenChange: (open: boolean) => void }
  | { controlled?: false; defaultOpen?: boolean; onOpenChange?: (open: boolean) => void };

function Dialog(props: DialogProps) {
  const isOpen = props.controlled ? props.open : props.defaultOpen ?? false;
  return <div data-open={isOpen} />;
}
```

### Mutually Exclusive Props Using `never`

```typescript
type IconOnlyButtonProps = {
  icon: React.ReactNode;
  label: string;
  children?: never;
};

type TextButtonProps = {
  children: React.ReactNode;
  icon?: never;
  label?: never;
};

type ButtonProps = (IconOnlyButtonProps | TextButtonProps) &
  React.ComponentPropsWithoutRef<"button">;

function Button(props: ButtonProps) {
  if ("icon" in props) {
    const { icon, label, ...buttonProps } = props;
    return <button aria-label={label} {...buttonProps}>{icon}</button>;
  }

  const { children, ...buttonProps } = props;
  return <button {...buttonProps}>{children}</button>;
}
```

Recommended: use `never` to prevent invalid prop combinations.

### Discriminated Union Props

```typescript
type NotificationProps =
  | { type: "success"; message: string; action?: never }
  | { type: "error"; message: string; action: { label: string; onClick: () => void } }
  | { type: "info"; message: string; action?: { label: string; onClick: () => void } };

function Notification(props: NotificationProps) {
  return (
    <div data-type={props.type}>
      {props.message}
      {props.action && <button onClick={props.action.onClick}>{props.action.label}</button>}
    </div>
  );
}
```

### Controlled vs Uncontrolled Component Prop Union

```typescript
type ControlledInputProps = {
  value: string;
  onValueChange: (value: string) => void;
  defaultValue?: never;
};

type UncontrolledInputProps = {
  defaultValue?: string;
  value?: never;
  onValueChange?: (value: string) => void;
};

type SmartInputProps = (ControlledInputProps | UncontrolledInputProps) &
  Omit<React.ComponentPropsWithoutRef<"input">, "value" | "defaultValue" | "onChange">;

function SmartInput(props: SmartInputProps) {
  const { onValueChange, ...rest } = props;

  return (
    <input
      {...rest}
      onChange={(event) => onValueChange?.(event.currentTarget.value)}
    />
  );
}
```

Pitfall: do not allow both `value` and `defaultValue` unless your component explicitly supports that behavior.

### Compound Components

A simple compound component can expose typed subcomponents as properties.

```typescript
type TabsProps = {
  children: React.ReactNode;
};

type TabsListProps = {
  children: React.ReactNode;
};

type TabsTriggerProps = React.ComponentPropsWithoutRef<"button"> & {
  value: string;
};

function TabsRoot({ children }: TabsProps) {
  return <div>{children}</div>;
}

function TabsList({ children }: TabsListProps) {
  return <div role="tablist">{children}</div>;
}

function TabsTrigger({ value, ...props }: TabsTriggerProps) {
  return <button role="tab" data-value={value} {...props} />;
}

export const Tabs = Object.assign(TabsRoot, {
  List: TabsList,
  Trigger: TabsTrigger,
});
```

Usage:

```typescript
function Example() {
  return (
    <Tabs>
      <Tabs.List>
        <Tabs.Trigger value="details">Details</Tabs.Trigger>
      </Tabs.List>
    </Tabs>
  );
}
```

Note: TypeScript can type subcomponent properties, but it does not enforce that only specific children appear inside a compound component at runtime.

### Higher-Order Component That Preserves Props

```typescript
function withLoading<P extends object>(
  Component: React.ComponentType<P>,
) {
  type Props = P & {
    isLoading?: boolean;
  };

  function WrappedComponent({ isLoading = false, ...props }: Props) {
    if (isLoading) return <p>Loading...</p>;
    return <Component {...(props as P)} />;
  }

  return WrappedComponent;
}
```

Note: HOCs often require a narrow assertion because TypeScript cannot always prove that rest props still equal `P` after destructuring. Keep assertions localized and avoid changing prop shapes unnecessarily.

Alternative with explicit injected props:

```typescript
type WithUserProps = {
  user: { id: string; name: string };
};

function withCurrentUser<P extends WithUserProps>(Component: React.ComponentType<P>) {
  type OuterProps = Omit<P, keyof WithUserProps>;

  function Wrapped(props: OuterProps) {
    const user = { id: "u1", name: "Ada" };
    return <Component {...({ ...props, user } as P)} />;
  }

  return Wrapped;
}
```

Recommended: prefer hooks over HOCs for new code unless you specifically need component wrapping.

### Type-Safe Component Maps

```typescript
type FieldType = "text" | "textarea";

type FieldProps = {
  name: string;
  label: string;
};

const fieldComponents: Record<FieldType, React.ComponentType<FieldProps>> = {
  text: ({ name, label }) => <label>{label}<input name={name} /></label>,
  textarea: ({ name, label }) => <label>{label}<textarea name={name} /></label>,
};

function Field({ type, ...props }: FieldProps & { type: FieldType }) {
  const Component = fieldComponents[type];
  return <Component {...props} />;
}
```

### Type-Safe Variants

```typescript
const buttonClasses = {
  primary: "btn btn-primary",
  secondary: "btn btn-secondary",
  danger: "btn btn-danger",
} as const;

type ButtonVariant = keyof typeof buttonClasses;

type VariantButtonProps = React.ComponentPropsWithoutRef<"button"> & {
  variant?: ButtonVariant;
};

function VariantButton({ variant = "primary", className, ...props }: VariantButtonProps) {
  return (
    <button
      className={[buttonClasses[variant], className].filter(Boolean).join(" ")}
      {...props}
    />
  );
}
```

Recommended: derive variant unions from constant maps when the map is the source of truth.

---

## 15. Common Mistakes

### Mistake: Overusing `any`

Problematic:

```typescript
type UserCardProps = {
  user: any;
};

function UserCard({ user }: UserCardProps) {
  return <div>{user.profile.displayName.toUpperCase()}</div>;
}
```

Why it is a problem: `any` disables type checking. Misspelled fields and invalid shapes become runtime errors.

Corrected:

```typescript
type User = {
  profile: {
    displayName: string;
  };
};

type UserCardProps = {
  user: User;
};

function UserCard({ user }: UserCardProps) {
  return <div>{user.profile.displayName.toUpperCase()}</div>;
}
```

Recommended: use `unknown` at boundaries, then narrow or validate.

### Mistake: Incorrect Children Typing

Problematic:

```typescript
type CardProps = {
  children: JSX.Element;
};

function Card({ children }: CardProps) {
  return <section>{children}</section>;
}

// Fails even though React can render text.
<Card>Plain text</Card>;
```

Why it is a problem: `JSX.Element` is too narrow for normal children.

Corrected:

```typescript
type CardProps = {
  children: React.ReactNode;
};

function Card({ children }: CardProps) {
  return <section>{children}</section>;
}
```

### Mistake: Incorrect Event Typing

Problematic:

```typescript
function Search() {
  function handleChange(event: Event) {
    console.log(event.target.value);
  }

  return <input onChange={handleChange} />;
}
```

Why it is a problem: DOM `Event` is not React's change event, and `target` is not safely typed as an input.

Corrected:

```typescript
function Search() {
  function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
    console.log(event.currentTarget.value);
  }

  return <input onChange={handleChange} />;
}
```

### Mistake: `useState([])` Becoming `never[]`

Problematic:

```typescript
function Tags() {
  const [tags, setTags] = React.useState([]);

  // May fail because tags can be inferred as never[].
  setTags(["react"]);

  return null;
}
```

Why it is a problem: an empty array has no element type information.

Corrected:

```typescript
function Tags() {
  const [tags, setTags] = React.useState<string[]>([]);

  setTags(["react"]);

  return <div>{tags.join(", ")}</div>;
}
```

### Mistake: Unsafe Context Defaults

Problematic:

```typescript
type AuthContextValue = {
  user: { id: string; name: string };
  logout: () => void;
};

const AuthContext = React.createContext<AuthContextValue>({} as AuthContextValue);
```

Why it is a problem: consumers can access missing fields if rendered outside the provider.

Corrected:

```typescript
const AuthContext = React.createContext<AuthContextValue | null>(null);

function useAuth() {
  const context = React.useContext(AuthContext);
  if (context === null) throw new Error("useAuth must be used within AuthContext.Provider");
  return context;
}
```

### Mistake: Confusing `JSX.Element`, `ReactNode`, and `ReactElement`

Problematic:

```typescript
type ModalProps = {
  title: React.ReactElement;
  children: JSX.Element;
};
```

Why it is a problem: titles and children often accept strings, numbers, fragments, arrays, or `null`; these types are too narrow.

Corrected:

```typescript
type ModalProps = {
  title: React.ReactNode;
  children: React.ReactNode;
};
```

Use `ReactElement` only when you need a concrete element:

```typescript
type TriggerProps = {
  trigger: React.ReactElement;
};
```

### Mistake: Incorrect Ref Typing

Problematic:

```typescript
function Input() {
  const ref = React.useRef<HTMLInputElement>();

  return <input ref={ref} />;
}
```

Why it is a problem: DOM refs are initially `null`, and the no-argument overload creates a ref whose current value may be `undefined`.

Corrected:

```typescript
function Input() {
  const ref = React.useRef<HTMLInputElement | null>(null);

  React.useEffect(() => {
    ref.current?.focus();
  }, []);

  return <input ref={ref} />;
}
```

### Mistake: Overusing `React.FC`

Problematic:

```typescript
type SelectProps<T> = {
  value: T;
  onChange: (value: T) => void;
};

// Awkward for generics.
const Select: React.FC<SelectProps<string>> = ({ value }) => {
  return <span>{value}</span>;
};
```

Why it is a problem: `React.FC` can be less ergonomic for generic components and does not remove the need to type `children` intentionally.

Corrected:

```typescript
type SelectProps<T> = {
  value: T;
  onChange: (value: T) => void;
};

function Select<T>({ value }: SelectProps<T>) {
  return <span>{String(value)}</span>;
}
```

### Mistake: Not Narrowing Nullable Values

Problematic:

```typescript
type User = { name: string };

function Profile({ user }: { user: User | null }) {
  return <h1>{user.name}</h1>;
}
```

Why it is a problem: `user` may be `null`.

Corrected:

```typescript
function Profile({ user }: { user: User | null }) {
  if (user === null) return <p>No user</p>;

  return <h1>{user.name}</h1>;
}
```

### Mistake: Incorrectly Typing Async Data

Problematic:

```typescript
type User = { id: string; name: string };

function Profile() {
  const [user, setUser] = React.useState<User>({} as User);

  return <h1>{user.name.toUpperCase()}</h1>;
}
```

Why it is a problem: the placeholder object is not a real `User`.

Corrected:

```typescript
type UserState =
  | { status: "loading" }
  | { status: "success"; user: User }
  | { status: "error"; error: Error };

function Profile() {
  const [state] = React.useState<UserState>({ status: "loading" });

  if (state.status === "loading") return <p>Loading...</p>;
  if (state.status === "error") return <p>{state.error.message}</p>;

  return <h1>{state.user.name.toUpperCase()}</h1>;
}
```

### Mistake: Assuming `response.json()` Is Automatically Type-Safe

Problematic:

```typescript
type User = { id: string; name: string };

async function getUser(): Promise<User> {
  const response = await fetch("/api/user");
  return response.json();
}
```

Why it is a problem: JSON is runtime data. TypeScript cannot verify the response shape.

Corrected:

```typescript
function isUser(value: unknown): value is User {
  return (
    typeof value === "object" &&
    value !== null &&
    "id" in value &&
    "name" in value &&
    typeof value.id === "string" &&
    typeof value.name === "string"
  );
}

async function getUser(): Promise<User> {
  const response = await fetch("/api/user");
  const value = (await response.json()) as unknown;

  if (!isUser(value)) throw new Error("Invalid user response");

  return value;
}
```

### Mistake: Creating Overly Broad Prop Types

Problematic:

```typescript
type ButtonProps = {
  variant: string;
  onClick: Function;
};
```

Why it is a problem: any string is allowed, and `Function` gives no useful parameter or return type safety.

Corrected:

```typescript
type ButtonProps = {
  variant: "primary" | "secondary" | "danger";
  onClick: React.MouseEventHandler<HTMLButtonElement>;
};
```

Recommended: use literal unions and specific function types.

---

## 16. Quick Reference Tables

### React Children Types

| Type | Use for | Accepts | Example |
|---|---|---|---|
| `React.ReactNode` | Normal children and visual slots | Anything React can render | `children: React.ReactNode` |
| `React.ReactElement` | A concrete element to inspect/clone | One React element | `trigger: React.ReactElement` |
| `React.ReactElement<P>` | A concrete element with expected props | One element with props `P` | `child: React.ReactElement<{ id: string }>` |
| `JSX.Element` | Explicit JSX return type | JSX expression result | `function App(): JSX.Element` |
| `React.PropsWithChildren<P>` | Add optional children to props | `P & { children?: ReactNode }` | `PropsWithChildren<{ title: string }>` |

Recommended: use `ReactNode` for most children. Use `ReactElement` only when you need an actual element object. Use `JSX.Element` mainly for component return annotations.

### Common Event Types

| Interaction | Event type | Element example |
|---|---|---|
| Button click | `React.MouseEvent<HTMLButtonElement>` | `<button onClick={...}>` |
| Div mouse enter | `React.MouseEvent<HTMLDivElement>` | `<div onMouseEnter={...}>` |
| Input change | `React.ChangeEvent<HTMLInputElement>` | `<input onChange={...}>` |
| Textarea change | `React.ChangeEvent<HTMLTextAreaElement>` | `<textarea onChange={...}>` |
| Select change | `React.ChangeEvent<HTMLSelectElement>` | `<select onChange={...}>` |
| Form submit | `React.FormEvent<HTMLFormElement>` | `<form onSubmit={...}>` |
| Input keydown | `React.KeyboardEvent<HTMLInputElement>` | `<input onKeyDown={...}>` |
| Input focus/blur | `React.FocusEvent<HTMLInputElement>` | `<input onBlur={...}>` |
| Div drag/drop | `React.DragEvent<HTMLDivElement>` | `<div onDrop={...}>` |
| Input paste | `React.ClipboardEvent<HTMLInputElement>` | `<input onPaste={...}>` |

### Common DOM Element Types

| JSX element | DOM type |
|---|---|
| `button` | `HTMLButtonElement` |
| `input` | `HTMLInputElement` |
| `textarea` | `HTMLTextAreaElement` |
| `select` | `HTMLSelectElement` |
| `form` | `HTMLFormElement` |
| `div` | `HTMLDivElement` |
| `span` | `HTMLSpanElement` |
| `a` | `HTMLAnchorElement` |
| `img` | `HTMLImageElement` |
| `ul` | `HTMLUListElement` |
| `li` | `HTMLLIElement` |
| `canvas` | `HTMLCanvasElement` |

### Common Utility and Helper Types

| Type | What it does | React use case |
|---|---|---|
| `Partial<T>` | Makes properties optional | Patch updates, draft forms |
| `Required<T>` | Makes properties required | Resolved defaults |
| `Pick<T, K>` | Selects keys | Preview props from a domain type |
| `Omit<T, K>` | Removes keys | Avoid native prop conflicts |
| `Record<K, T>` | Maps keys to values | Variant maps, component maps |
| `Readonly<T>` | Prevents property assignment | Immutable props/contracts |
| `NonNullable<T>` | Removes `null` and `undefined` | Values after narrowing |
| `ReturnType<T>` | Extracts function return | State from factory functions |
| `Parameters<T>` | Extracts function args tuple | Reusing callback argument types |
| `Awaited<T>` | Extracts promise result | API response types from async helpers |
| `ComponentProps<T>` | Gets component/element props | Mirroring props |
| `ComponentPropsWithoutRef<T>` | Gets props without ref | DOM wrappers without refs |
| `ComponentPropsWithRef<T>` | Gets props with ref | Ref-forwarding wrappers |
| `ElementRef<T>` | Gets ref target type | Component/intrinsic refs |

### Hooks and Their Type Patterns

| Hook | Typical type pattern | Example |
|---|---|---|
| `useState` | Infer simple values | `useState("")` |
| `useState<T>` | Explicit for null/empty arrays/unions | `useState<User \| null>(null)` |
| `useReducer` | Explicit state/action via reducer | `useReducer(reducer, initialState)` |
| `useRef<T \| null>` | DOM refs | `useRef<HTMLInputElement \| null>(null)` |
| `useRef<T>` | Mutable values | `useRef(0)` |
| `useContext` | Context type from `createContext` | `useContext(AuthContext)` |
| `useMemo<T>` | Rare explicit type for complex values | `useMemo<AuthValue>(() => value, [deps])` |
| `useCallback` | Usually inferred from function | `useCallback((id: string) => {}, [])` |
| Custom hook tuple | Explicit tuple or `as const` | `return [value, setValue] as const` |
| Custom hook object | Explicit return type for API stability | `function useX(): UseXReturn` |

### Native HTML Prop Helper Types

| Helper | Use for | Example |
|---|---|---|
| `React.ComponentPropsWithoutRef<"button">` | Button wrapper without ref | `type Props = ComponentPropsWithoutRef<"button">` |
| `React.ComponentPropsWithRef<"input">` | Input wrapper with ref | `forwardRef<HTMLInputElement, Props>` |
| `React.ButtonHTMLAttributes<HTMLButtonElement>` | Button attributes | `type Props = ButtonHTMLAttributes<HTMLButtonElement>` |
| `React.InputHTMLAttributes<HTMLInputElement>` | Input attributes | `type Props = InputHTMLAttributes<HTMLInputElement>` |
| `React.AnchorHTMLAttributes<HTMLAnchorElement>` | Anchor attributes | `type Props = AnchorHTMLAttributes<HTMLAnchorElement>` |
| `React.HTMLAttributes<HTMLDivElement>` | Generic div attributes | `type Props = HTMLAttributes<HTMLDivElement>` |
| `React.LabelHTMLAttributes<HTMLLabelElement>` | Label attributes | `type Props = LabelHTMLAttributes<HTMLLabelElement>` |
| `React.FormHTMLAttributes<HTMLFormElement>` | Form attributes | `type Props = FormHTMLAttributes<HTMLFormElement>` |

Recommended: prefer specific native helpers over generic `HTMLAttributes` for interactive elements.

### Common `useState` Typing Scenarios

| Scenario | Pattern | Example |
|---|---|---|
| Simple string | Inference | `const [name, setName] = useState("")` |
| Simple number | Inference | `const [count, setCount] = useState(0)` |
| Boolean | Inference | `const [open, setOpen] = useState(false)` |
| Nullable object | Explicit generic | `useState<User \| null>(null)` |
| Empty array | Explicit generic | `useState<Todo[]>([])` |
| Object with full initial shape | Inference or explicit | `useState({ query: "", page: 1 })` |
| Literal union | Explicit generic | `useState<"idle" \| "loading">("idle")` |
| Async state machine | Discriminated union | `useState<AsyncState<User>>({ status: "idle" })` |
| Derived expensive initial state | Lazy initializer | `useState(() => createInitialState())` |

### Common Ref Typing Scenarios

| Scenario | Pattern | Example |
|---|---|---|
| Input DOM ref | `T \| null` with `null` initial value | `useRef<HTMLInputElement \| null>(null)` |
| Button DOM ref | `T \| null` with `null` initial value | `useRef<HTMLButtonElement \| null>(null)` |
| Div DOM ref | `T \| null` with `null` initial value | `useRef<HTMLDivElement \| null>(null)` |
| Timer ref | `ReturnType<typeof setTimeout> \| null` | `useRef<ReturnType<typeof setTimeout> \| null>(null)` |
| Mutable counter ref | Inferred number | `useRef(0)` |
| Previous value ref | `T \| undefined` or `T \| null` | `useRef<string \| undefined>(undefined)` |
| Forwarded DOM ref | `forwardRef<Element, Props>` | `forwardRef<HTMLInputElement, Props>(...)` |
| Imperative handle | Custom handle type | `forwardRef<SearchHandle, Props>(...)` |
| Extract component ref | `ElementRef<typeof Component>` | `type Ref = ElementRef<typeof Input>` |

```typescript
const inputRef = React.useRef<HTMLInputElement | null>(null);
const timerRef = React.useRef<ReturnType<typeof setTimeout> | null>(null);
```

---

## Final Practical Rules

### Prefer Inference When

```typescript
const [name, setName] = React.useState("");
const [count, setCount] = React.useState(0);
const isDisabled = status === "loading";
```

Inference is preferred for obvious local variables, simple state initialized with representative values, inline event handlers, and derived values.

### Write Explicit Types When

```typescript
type Props = {
  userId: string;
  onSave: (value: string) => void;
};

type State =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; error: Error };
```

Explicit types are useful for component props, reusable hooks, exported functions, context values, reducers, nullable state, empty arrays, discriminated unions, async state, and public APIs.

### Avoid `any`

```typescript
function isStringArray(value: unknown): value is string[] {
  return Array.isArray(value) && value.every((item) => typeof item === "string");
}
```

Use `unknown`, generics, validators, and narrowing instead of `any`.

### Avoid Unsafe Assertions

```typescript
// Avoid:
const user = JSON.parse(raw) as User;

// Recommended:
const value = JSON.parse(raw) as unknown;
if (!isUser(value)) throw new Error("Invalid user");
const user = value;
```

Assertions are acceptable only when TypeScript lacks information that your code genuinely guarantees. Keep them narrow and close to the boundary.

### Model Impossible States with Discriminated Unions

```typescript
type DataState<T> =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: Error };
```

Avoid independent flags that can contradict each other.

```typescript
// Avoid: can represent impossible states.
type BadState<T> = {
  isLoading: boolean;
  data?: T;
  error?: Error;
};
```

### Type Reusable Components Without Losing Native Props

```typescript
type ButtonProps = React.ComponentPropsWithoutRef<"button"> & {
  variant?: "primary" | "secondary";
};

function Button({ variant = "primary", ...props }: ButtonProps) {
  return <button data-variant={variant} {...props} />;
}
```

Use native prop helpers and `Omit` conflicts.

### Safely Type Nullable Values

```typescript
function UserName({ user }: { user: User | null }) {
  if (user === null) return null;
  return <span>{user.name}</span>;
}
```

Narrow nullable values before use. Optional chaining is useful for display, but explicit branches are clearer when rendering different UI states.

### Choose `ReactNode`, `ReactElement`, and `JSX.Element` Correctly

```typescript
type LayoutProps = {
  children: React.ReactNode;
  trigger: React.ReactElement;
};

function Title({ text }: { text: string }): JSX.Element {
  return <h1>{text}</h1>;
}
```

Recommended: `ReactNode` for renderable content, `ReactElement` for a single element object, and `JSX.Element` for explicit component return types.
