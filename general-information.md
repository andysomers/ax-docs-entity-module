# General information

## Artifact {#module-artifact}

```xml
    <dependencies>
        <dependency>
            <groupId>com.foreach.across.modules</groupId>
            <artifactId>entity-module</artifactId>
            <version>{{ book.moduleVersion }}</version>
        </dependency>
    </dependencies>
```

## Module dependencies {#module-dependencies}

| Module | Type | Description |
| --- | --- | --- |
| AdminWebModule | optional | Enables auto generated forms for managing the registered entities. |

## Module settings {#module-settings}

| Property | Description | Default |
| --- | --- | --- |
| entityModule.entityValidator.registerForMvc | Should the entity Validator instance be registered as the default validator for MVC databinding. | true |



