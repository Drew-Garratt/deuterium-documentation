---
description: Performant, flexible and extensible forms with easy-to-use validation.
---

# React Hook Form

## Introduction

Forms are often a complex part of the UX development process. React Hooks forms attempts to simplify this process by providing a simple and lightweight hooks based approach to form.

## Example Usage

Principle interaction with React Hook Form is via the `useForm` hook. This hook allows us to create the field registration function, submit function and formstate.

```typescript
interface LoginFormInput {
  email: string;
  password: string;
}
const {
    register,
    handleSubmit,
    formState: { errors },
} = useForm<LoginFormInput>();
```

In the above example, we create a new type interface for our form fields.

We pass this interface as a type assertion to `useForm` allowing it to correctly type our form state.

We also define a register function and a handle submit function.

As you can see from the below. We can use our register function to register each form field with our hook. Allowing it to track, hold, validate and submit these values.

```tsx
const onSubmit: SubmitHandler<LoginFormInput> = (data) => {
  customerSignIn({ email: data.email, password: data.password });
};

<form onSubmit={handleSubmit(onSubmit)}>
  <label>
    Email
    <input
      {...register('email', { required: true })}
      disabled={loading}
    />
    {errors.email && 'Email is required'}
  </label>
  
  <label>
    Password
    <input
      type={'password'}
      {...register('password', { required: true })}
      disabled={loading}
    />
    {errors.password && 'Password is required'}
  </label>
</form>
```

React Form Hooks API is relatively straightforward making form handling a much more straight forward prospect.

## Recomended Reading

{% embed url="https://react-hook-form.com/get-started" %}
General Setup
{% endembed %}

