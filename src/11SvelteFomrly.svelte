<script>
  import { get } from "svelte/store";
  import { valuesForm, Field } from "svelte-formly";

  const fields = [
    {
      type: "input",
      name: "name",
      attributes: {
        type: "text",
        label: "Name",
        placeholder: "What is your name",
      },
      rules: ["required", "min:6"],
      messages: {
        required: "Name is required",
        min: "Name must have more that 6 caracters",
      },
    },

    {
      type: "input",
      name: "email",
      attributes: {
        type: "email",
        label: "Email",
        placeholder: "What is your email",
      },
      rules: ["required", "email"],
      messages: {
        required: "Email is required",
        email: "Email is invalid",
      },
    },
  ];

  let values = {};
  const data = get(valuesForm);

  console.log(data);

  function onSubmit() {
    const data = get(valuesForm);
    if (data.valid) {
      console.log(data);
      values = data.values;

      alert(JSON.stringify(values));
    }
  }
</script>

<form on:submit|preventDefault={onSubmit}>
  <Field {fields} />
  <button type="submit">Submit</button>
</form>
