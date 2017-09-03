== General information

=== Artifact
[source,xml,indent=0]
[subs="verbatim,quotes,attributes"]
----
	<dependencies>
		<dependency>
			<groupId>com.foreach.across.modules</groupId>
			<artifactId>{module-artifact}</artifactId>
			<version>{module-version}</version>
		</dependency>
	</dependencies>
----

=== Module dependencies

.Module dependencies
|===
|Module |Type |Description

|<<integration:adminwebmodule>>
|optional
|Enables auto generated forms for managing the registered entities.
|===

=== Module settings

|===
|Property |Description |Default

|entityModule.entityValidator.registerForMvc
|Should the entity Validator instance be registered as the default validator for MVC databinding.
|true
|===