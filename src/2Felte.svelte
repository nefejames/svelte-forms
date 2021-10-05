<script>
  import { createForm } from "felte";
  import { validator } from "@felte/validator-yup";
  import * as yup from "yup";

  const schema = yup.object({
    email: yup.string().email().required(),
    name: yup.string().required(),
  });

  const { form, errors } = createForm({
    extend: validator,
    validateSchema: schema,
    onSubmit: async (values) => {
      alert(JSON.stringify(values));
    },
  });
</script>

<form use:form on:submit|preventDefault>
  <input type="text" name="name" />
  {#if $errors.name}
    <span class="error">{$errors.name}</span>
  {/if}
  <input type="email" name="email" />
  {#if $errors.email}
    <span class="error">{$errors.email}</span>
  {/if}

  <button type="submit">Submit</button>
</form>
