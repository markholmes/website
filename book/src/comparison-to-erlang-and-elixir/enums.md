# Enums

Enums in Gleam are a way of modeling data that can be one of a few different
variants.

We've seen an enum already in this chapter- `Bool`. In Gleam Bool is defined
like this:

```
// A Bool is a value that is either `True` or `False`
enum Bool =
  | True
  | False
```

Enum variants can also contain other values.

```
enum User =
  | LoggedIn(String)  // A logged in user with a name
  | Guest             // A guest user with no details
```

```
let sara = LoggedIn("Sara")
let rick = LoggedIn("Rick")
let visitor = Guest
```

When given an enum we need to pattern match on it to determine the variant and
use any contained values.

```
fn get_name(user) {
  case user {
  | LoggedIn(name) -> name
  | Guest -> "Guest user"
  }
}
```

## Runtime representation

At runtime enum variants with no contained values become atoms. The atoms are
written in `snake_case` rather than `CamelCase` so `LoggedIn` becomes
`logged_in`.

Enum variants with contained values become tuples with a tag atom.

```
// Gleam
Guest
LoggedIn("Kim")
```
```
# Elixir
:guest
{:logged_in, "Kim"}
```
```
% Erlang
guest.
{logged_in, <<"Kim">>}.
```