Adding [tests](/docs/building-a-dbt-project/tests) to a project helps validate that your models are working correctly. So let's add some tests to our project!

1. Create a new YAML file in the `models` directory, named `models/schema.yml`
2. Add the following contents to the file:

<File name='models/schema.yml'>

```yaml
version: 2

models:
  - name: customers
    columns:
      - name: customer_id
        tests:
          - unique
          - not_null

  - name: stg_customers
    columns:
      - name: customer_id
        tests:
          - unique
          - not_null

  - name: stg_orders
    columns:
      - name: order_id
        tests:
          - unique
          - not_null
      - name: status
        tests:
          - accepted_values:
              values: ['placed', 'shipped', 'completed', 'return_pending', 'returned']
      - name: customer_id
        tests:
          - not_null
          - relationships:
              to: ref('stg_customers')
              field: customer_id

```

</File>

3. Execute `dbt test`, and confirm that all your tests passed.

<CloudCore>
    <Lightbox src="/img/successful-tests-dbt-cloud.png" title="Passing tests when using dbt Cloud" />
    <Lightbox src="/img/successful-tests-dbt-cli.png" title="Passing tests when using the dbt CLI" />
</CloudCore>

:::info

When you run `dbt test`, dbt iterates through your YAML files, and constructs a query for each test. Each query will return the number of records that fail the test. If this number is 0, then the test is successful.

:::

#### FAQs

<FAQ src="available-tests" alt_header="What tests are available for me to use in dbt? Can I add my own custom tests?" />
<FAQ src="test-one-model" />
<FAQ src="failed-tests" />
<FAQ src="schema-yml-name" alt_header="Does my test file need to be named `schema.yml`?" />
<FAQ src="multiple-test-files" />
<FAQ src="why-version-2" />
<FAQ src="recommended-tests" />
<FAQ src="when-to-test" />