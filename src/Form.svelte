<script>
  import * as Yup from "yup";

  const schema = Yup.object().shape({
    name: Yup.string().required("Name is required!"),
    email: Yup.string().email().required("Email is required"),
  });

  const onSubmit = (values) => {
    alert(JSON.stringify(values));
  };
</script>

<div class="container">
  <form on:submit|preventDefault>
    <div class="form-row">
      <label for="name">Name</label>
      <input type="name" name="name" />
    </div>
    <div class="form-row">
      <label for="email">Email</label>
      <input type="email" name="email" />
    </div>

    <button type="submit">Sign In</button>
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
