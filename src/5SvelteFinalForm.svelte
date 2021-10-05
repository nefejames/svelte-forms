<script>
  import { Form, Field } from "svelte-final-form";

  const initialValues = {
    name: "Nefe",
    email: "nefejames@yahoo.com",
  };

  const onSubmit = (values) => {
    alert(JSON.stringify(values));
  };

  const validate = (values) => {
    const errors = {};
    if (!values.name) {
      errors.name = "Name is required";
    }
    if (!values.email) {
      errors.email = "Email is Required";
    } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(values.email)) {
      errors.email = "Invalid emaill address";
    }
    return errors;
  };
</script>

<Form {onSubmit} {validate} {initialValues} let:form let:state>
  <form on:submit|preventDefault={form.submit}>
    <Field name="name" let:input let:meta>
      <label for="name">Name</label>
      <input
        name={input.name}
        on:blur={input.onBlur}
        on:focus={input.onFocus}
        on:input={(e) => input.onChange(e.target.value)}
        type="text"
        value={input.value}
      />
      {#if meta.touched && meta.error}
        <span class="error">{meta.error}</span>
      {/if}
    </Field>

    <Field name="email" let:input let:meta>
      <label for="email">Name</label>
      <input
        name={input.email}
        on:blur={input.onBlur}
        on:focus={input.onFocus}
        on:input={(e) => input.onChange(e.target.value)}
        type="text"
        value={input.value}
      />
      {#if meta.touched && meta.error}
        <span class="error">{meta.error}</span>
      {/if}
    </Field>

    <button type="submit" disabled={state.submitting}>Submit</button>
  </form>
</Form>
