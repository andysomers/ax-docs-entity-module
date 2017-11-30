# What's new in this version?

## 2.2.1-SNAPSHOT

* it is now possible to configure default view element modes \(eg. control or readonly rendering\) on an `EntityConfiguration`
  * these will be used in all cases where no specific configuration has been configured on property level

## 2.2.0.RELEASE

* added [message codes](/appendix/message-codes.md) for admin menu items 
  * of the entity management section
  * of a group of entities \(defaults to the module name\)
  * of a single entity type
* [EntityQuery Language](/entityquery-infrastructure.md) allows specifying an order by clause or a `Sort` specifier
* `OptionIterableBuilder` can return a sorted specification by implementing the isSorted\(\) method
  * if the `OptionGenerator` has no explicit sorting parameter set, it now only sorts if the configured `OptionIterableBuilder` is not sorted
  * if you specify option values using an EQL statement, the sort specifier of your `EntityQuery` will be taken into account
* [EntityQuery filtering](/entityquery-infrastructure.md) now supports a basic and advanced mode to support the use of configured property filters and the use of eql statements

## 2.1.0.RELEASE

* improve the ability to [customize page titles and layouts](/customizing-entity-views.md)
  * all entity views now set a page \(sub\) title if a matching message code returns a non-empty string
    * there is a default title for all views except the list view
  * list views now also publish an `EntityPageStructureRenderedEvent`
* select option controls now support `SelectFormElementConfiguration` to render more advanced bootstrap-select controls
* added _ILIKE_ operator to the [EntityQuery Language](/entityquery-infrastructure.md) for case insensitive matching on String columns
  * an `EntityQueryConditionTranslator` attribute can be registered on entity properties to ensure regular equal and like lookups are always converted to the case insensitive equivalent

## 2.0.0.RELEASE

This release has a lot of breaking changes compared with the previous release.  
The code has been heavily rewritten and optimized.  
The public API modified accordingly with a focus on simplification and future extensibility.

* requires Across 2.0.0+
* massive overhaul of the `EntitiesConfigurationBuilder` system - removed the `and()` concatenating of builder calls
* massive overhaul of `EntityViewFactory`, `EntityViewProcessor` and the default administration controllers
  * nested builder consumers are used instead - this greatly simplified the class hierarchy involved
  * externalized the entire `ViewElement` infrastructure to BootstrapUiModule
  * if BootstrapUiModule is not present, default views will not be created
* compatibility update with Spring 4.2 which replaces `CrudInvoker` with `RepositoryInvoker` from spring-data-commons.
* principal names on `Auditable` entities are now pretty printed using the `SecurityPrincipalLabelResolverStrategy` from the _SpringSecurityModule_
* EntityModule now supports deleting of entities
* the `EntityModel` of an `EntityConfiguration` can now be customized using the `EntityConfigurer` builders
* extension of the [EntityQuery infrastructure](/entityquery-infrastructure.md)
  * addition of the EntityQuery Language \(EQL\) providing SQL-like syntax for building an `EntityQuery`
  * provide a default EQL-based filter for list views
* addition of the entity browser in the _Developer tools_ section of AdminWebModule
  * allows seeing all registered entities along with their attributes, properties, views and associations
  * the entity browser is only activate if development mode is active
* streamlined the message code hierarchy for view rendering, see [appendix for details](/appendix/message-codes.md)
* a list view can now have a default predicate assigned using an EQL statement
  * this can be used to ensure a list result always has a default filter applied
* default entity views support transactions, allowing multiple processors to modify data in a single transaction
  * transactions are enabled by default for state modifying HTTP methods of all form views \(create, update, delete and custom form views\)
* option controls \(select, multi-checkbox\) can be easily customized through a number of attributes
  * making it easier to specify the option values that can be selected



