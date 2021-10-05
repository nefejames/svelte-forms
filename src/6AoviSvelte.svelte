<script>
  import { aoviSvelte } from "aovi-svelte";

  // Create the aoviSvelte store that has object of values to be validated
  const form = aoviSvelte({
    name: "",
    email: "",
  });

  function handleSubmit() {
    // Run aovi validators

    form.aovi.check("name").required().minLength(4).check("email").required()
      .end;

    if ($form.valid) {
      // when aovi checks was successful, do thing
      let formData = `The user's name is ${$form.name} and their email is ${$form.email}`;
      alert(JSON.stringify(formData));
    }
  }
</script>

<div class="container">
  <form on:submit|preventDefault={handleSubmit}>
    <div class="form-row">
      <label for="name"> Name </label>
      <input name="name" bind:value={$form.name} class:error={$form.err.name} />
      {#if $form.err.name}
        <span class="error">{$form.err.name}</span>
      {/if}
    </div>

    <div class="form-row">
      <label for="email">Email</label>
      <input
        name="email"
        bind:value={$form.email}
        class:error={$form.err.email}
      />
      {#if $form.err.email}
        <span class="error">{$form.err.email}</span>
      {/if}
    </div>

    <button>Submit</button>
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
