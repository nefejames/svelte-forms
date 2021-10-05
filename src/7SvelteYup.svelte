<script>
  import * as yup from "yup";
  import { Form, Message } from "svelte-yup";
  let schema = yup.object().shape({
    name: yup.string().required().min(6).max(30).label("Name"),
    email: yup.string().required().email().label("Email address"),
  });
  let fields = { name: "", email: "" };
  let submitted = false;
  let isValid;
  function formSubmit() {
    submitted = true;
    isValid = schema.isValidSync(fields);
    if (isValid) {
      alert(JSON.stringify(fields));
    }
  }
</script>

<Form class="form" {schema} {fields} submitHandler={formSubmit} {submitted}>
  <input type="text" bind:value={fields.name} placeholder="Name" />
  <Message name="name" />
  <input type="text" bind:value={fields.email} placeholder="Email address" />
  <Message name="email" />
  <button type="submit">Submit</button>
</Form>
