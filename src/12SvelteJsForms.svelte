<script>
  import { Form, Input } from "sveltejs-forms";
  import * as yup from "yup";

  function handleSubmit({ detail: { values, setSubmitting, resetForm } }) {
    alert(JSON.stringify(values));
    setSubmitting(false);
    resetForm({ name: "", email: "" });
  }

  let schema = yup.object().shape({
    name: yup.string().required().label("Name"),
    email: yup.string().required().email().label("Email address"),
  });
</script>

<Form
  {schema}
  validateOnBlur={false}
  validateOnChange={false}
  on:submit={handleSubmit}
>
  <Input name="name" type="text" label="Name" placeholder="Name" />
  <Input name="email" label="Email Address" placeholder="Email" />

  <button type="submit">Sign in</button>
</Form>

<style>
  :global(.sveltejs-forms) {
    background-color: #f8f8f8;
    display: inline-block;
    padding: 1rem;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  :global(label) {
    font-size: 0.8rem;
    color: #888;
    margin-bottom: 0.2rem;
  }

  :global(.message) {
    font-size: 0.8rem;
    color: #888;
    margin: 0.2rem 0;
    color: #f56565;
  }

  :global(input[type="text"]),
  :global(textarea),
  :global(select) {
    width: 100%;
    background-color: white;
    margin: 0;
  }

  :global(input[type="checkbox"] + label) {
    display: inline-block;
    margin-right: 2rem;
  }

  :global(.field) {
    margin-bottom: 1rem;
  }

  button {
    border-radius: 5px;
    padding: 0.5rem 1rem;
    margin-right: 1rem;
    color: white;
  }

  button[type="submit"] {
    background-color: #48bb78;
  }
</style>
