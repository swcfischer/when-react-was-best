# When React Was Best

I may add more code examples to this `readme.md`

This project puts two React styles side by side: a hooks-based auth page with
styled components and a classical class component with SCSS and `clsx`. The
classical version is a reminder of a frontend style that valued visible
structure and straightforward tools.

## Why the classical style still feels good

### State is easy to scan

In [AuthPageClassical.jsx](./AuthPageClassical.jsx), the page's state is declared
as one object, not many useState declarations with arrays and a getter value and setter.

```jsx
this.state = {
  isRegistering: false,
  name: "",
  email: "",
  password: "",
  error: "",
  isSubmitting: false,
};
```

By comparison, the hooks version declares each value with a separate
`useState` call. Both are valid; the single state object just makes this
component's inventory feel especially explicit.

### BEM makes the markup and styles correspond

The SCSS in [AuthPageClassical.scss](./AuthPageClassical.scss) follows the same
block, element, modifier structure. Take note of ampersand syntax:

```scss
.auth-page {
  &__form {
    display: grid;
  }

  &__submit {
    background: var(--color-accent);

    &--submitting {
      cursor: wait;
    }
  }
}
```

`clsx` adds the modifier only when it applies. This keeps styling in a
stylesheet, while the component markup stays recognizable as HTML with
descriptive class names.

### Styling imports look like styling

The hooks-based [AuthPage.jsx](./AuthPage.jsx) imports names such as `AuthFrame`,
`Heading`, and `SaveButton` from `NoteEditor.styles.jsx`. Those names look like
ordinary React components even though they are styling primitives. A long
import list can take attention away from the page's actual UI and behavior.
With SCSS, one stylesheet import and BEM class names make the separation
obvious:

## Handler naming

```jsx
// From lines 26 in AuthPage.jsx
async function submit(event) {
  event.preventDefault();
  setIsSubmitting(true);
  setError("");

  try {
    if (isRegistering) {
      await register({ name, email, password });
    } else {
      await login({ email, password });
    }
  } catch (submitError) {
    setError(submitError.message || "Couldn't authenticate.");
  } finally {
    setIsSubmitting(false);
  }
}
```

`submit` should be `handleSubmit` makes clear that the function handles the form event.
