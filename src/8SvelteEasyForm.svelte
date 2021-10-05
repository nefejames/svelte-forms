<script>
  import createForm from "@vkhalikov/svelte-easy-form";

  const required = (message) => (val) => {
    if (!val) {
      return message;
    }

    return null;
  };

  const email = (message) => (val) => {
    const emailRegex = /^[\w-.]+@([\w-]+\.)+[\w-]{2,4}$/g;
    if (!emailRegex.test(val)) {
      return message;
    }
    return null;
  };

  const schema = {
    Name: {
      validators: [required("Name is required")],
      type: "text",
    },
    Email: {
      validators: [required("Email is required"), email("Invalid email")],
      type: "email",
    },
  };

  const { values, errors, onInput, onSubmit } = createForm(schema);

  console.log($errors);
</script>

<div class="container">
  <h1>svelte-easy-form</h1>

  <form on:submit|preventDefault={onSubmit}>
    {#each Object.entries(schema) as [name, { type }]}
      <div class="form-row">
        <label for={name} class="form-label text-capitalize">{name}</label>
        <input
          {type}
          {name}
          class="form-control"
          value={$values[name]}
          on:input={onInput}
        />

        {#if $errors[name]}
          <span class="error">{$errors[name]}</span>
        {/if}
      </div>
    {/each}

    <button class="btn btn-secondary" type="submit">Submit</button>
  </form>
</div>

<style lang="scss">
  $primary-color: #1d3557;
  $error-color: #e63946;
  $bg-color: #e6e7e5;
  $text-color: #293241;
  $color-white: #fff;
  $border-radius: 4px;

  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    list-style: none;
  }

  :global(body) {
    font-family: 62.5%;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    height: 100vh;
    background: $bg-color;
    display: flex;
    justify-content: center;
  }

  .container {
    margin-top: 5rem;
    padding: 3rem;
    width: 400px;
    border-radius: $border-radius;

    label,
    input {
      color: $text-color;
    }

    label {
      font-size: 1.2rem;
      margin-bottom: 0.5rem;
    }

    input {
      border: 2px solid rgba($primary-color, 0.8);
      border-radius: $border-radius;
      padding: 0.5rem 1rem;
      padding-left: 1rem;
      font-size: 1rem;
    }

    .form-row {
      display: flex;
      flex-direction: column;
      margin-bottom: 1.5rem;
    }

    button {
      color: $color-white;
      width: 100%;
      font-size: 1.4rem;
      background: $primary-color;
      border-radius: $border-radius;
      border: none;
      cursor: pointer;
      padding: 0.4rem 1.2rem;
      margin-top: 0.5rem;

      &:hover {
        background: rgba($primary-color, 0.8);
      }
    }

    .error {
      color: $error-color;
      font-size: 1rem;
      margin-top: 0.3rem;
    }

    .disabled-btn {
      cursor: not-allowed;
      background: rgba($primary-color, 0.8);
    }
  }
</style>
