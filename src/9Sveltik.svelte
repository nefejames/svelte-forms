
<script>
  import { Sveltik, Form, Field, ErrorMessage } from 'sveltik'

  let initialValues = {
    name: '',
    email: '',
  }

  let validate = values => {
    const errors = {}
    if(!values.name){
      errors.name = "Name is required"
    }
    if (!values.email) {
        errors.email = 'Email is required'
    } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)) {
        errors.email = 'Invalid email address'
        }
      return errors
    }

    let onSubmit = (values) => {
        setTimeout(() => {
            alert(JSON.stringify(values, null, 2))
            setSubmitting(false)
        }, 400)
    }
</script>

<Sveltik {initialValues} {validate} {onSubmit}>
  <Form>
    <div class="form-row">
      <Field type="text" name="name" />
      <ErrorMessage name="name" as="span" />
    </div>

    <div class="form-row">
      <Field type="email" name="email" />
      <ErrorMessage name="email" as="span" />
    </div>
    
    <button type="submit">Submit</button>
  </Form>
</Sveltik>