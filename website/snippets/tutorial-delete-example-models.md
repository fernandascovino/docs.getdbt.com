We don't need the sample files that dbt created for us anymore! Let's delete them.

1. Delete the `models/example/` directory
2. Delete the `example:` key from your `dbt_project.yml` file, and any configurations that are listed under it

<File name='dbt_project.yml'>

```yaml
# before
models:
  jaffle_shop:
    +materialized: table
    example:
      +materialized: view
```

</File>

<File name='dbt_project.yml'>

```yaml
# after
models:
  jaffle_shop:
    +materialized: table
```

</File>

#### FAQs

<FAQ src="removing-deleted-models" />
<FAQ src="unused-model-configurations" />