<script>
	import { formula } from "svelte-formula";
	const { form, formValues, validity, formValid } = formula();

	formValues.subscribe(v => console.log(v));
</script>

<form use:form>
  <div class='form-row'>
    <label for='username'>Username</label>
    <input type='text' id='username' name='username' required minlength="8"/>
    <span hidden={$validity?.username?.valid}>{$validity?.username?.message}</span>
  </div>
  <div class='form-row'>
    <label for='password'>Password</label>
    <input type='password' id='password' name='password' required minlength="8" />
    <span  hidden={$validity?.password?.valid}>{$validity?.password?.message}</span>
  </div>

  <button disabled={!$formValid}>Save</button>
</form>