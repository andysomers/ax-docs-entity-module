=== EntityLinkBuilder

An `EntityConfiguration` or `EntityAssociation` can have one or more `EntityLinkBuilder` instances registered in its attributes.
An `EntityLinkBuilder` is used to create application links to management controllers for the entity.
By default the `EntityModule` will create an `EntityLinkBuilder` for the management pages in admin web if `AdminWebModule` is present, and this link builder will be registered as the attribute with `EntityLinkBuilder` class as key.

You can use the `EntityLinkBuilder` directly for example in redirects, often the specific `EntityLinkBuilder` is overridable per view.
All links the `EntityLinkBuilder` generates are entirely configurable, please refer to the javadoc for all possible settings.

[source,java,indent=0]
[subs="verbatim,quotes,attributes"]
----
EntityLinkBuilder linkBuilder = entityConfiguration.getAttribute( EntityLinkBuilder.class );

// Will create a link of the form "/entities/{parent}/{parentId}/update"
String path = linkBuilder.update( parent );
----

==== EntityLinkBuilder for associations
Associations usually also have an `EntityLinkBuilder` registered, it is possible to create links to items that are an association from a parent entity.
To achieve this you must _scope_ the `EntityLinkBuilder` to the parent entity it belongs to.

[source,java,indent=0]
[subs="verbatim,quotes,attributes"]
----
EntityLinkBuilder linkBuilder = entityConfiguration.getAttribute( EntityLinkBuilder.class );

EntityConfiguration associated = association.getTargetEntityConfiguration();
EntityLinkBuilder associatedLinkBuilder = association.getAttribute( EntityLinkBuilder.class )
                                                     .asAssociationFor( linkBuilder, parent );

// Will create a link of the form "/entities/{parent}/{parentId}/associations/{associationName}/{childId}/update"
String path = associatedLinkBuilder.update( child );
----