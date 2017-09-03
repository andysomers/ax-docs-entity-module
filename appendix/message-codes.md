# Message codes

Labels are resolved using a message code hierarchy.
Simply define one or more message sources specifying the properties you want.
Unless custom `EntityMessageCodeResolver` instances are being used, message codes are generated as follows:

|Message code|Description|
|---|---|
| enums.*EnumName*.*EnumValue*| Message code for a single enum value label. <br> Example: _enums.Numbers.ONE_|
| *EntityPrefix*.name.singular| Label for an entity in singular form, for use outside or at the beginning of a sentence. <br>Example: _UserModule.entities.user.name.singular_ |
| *EntityPrefix*.name.plural | Label for an entity in plural form, for use outside or at the beginning of a sentence. <br>Example: _UserModule.entities.user.name.plural_ |
| *EntityPrefix*.name.singular.inline| Label for an entity in singular form, for use within a sentence. If not explicitly specified, the label is generated based by lower-casing the non-inline version. <br>Example: UserModule.entities.user.name.singular.inline_|
| *EntityPrefix*.name.plural.inline| Label for an entity in plural form, for use within a sentence.  If not explicitly specified, the label is generated based by lower-casing the non-inline version. <br>Example: _UserModule.entities.user.name.plural.inline_|
| *EntityPrefix*.properties.*propertyName*| Label for a single entity property. <br>Example: _UserModule.entities.user.properties.username_|
| *EntityPrefix*.properties.*propertyName*[description]| Description text for a property.  If not empty this will be rendered in a help block on forms. <br>Example: _UserModule.entities.user.properties.username[description]_|
| *EntityPrefix*.properties.*propertyName*[placeholder]| Placeholder text for a property.  Will be used for certain controle like textbox. <br>Example: _UserModule.entities.user.properties.username[placeholder]_|
| *EntityPrefix*.validation.*validatorKey*| Description text for a validation error message.  Optionally can be suffixed with the specific property name. <br>Example: _UserModule.entities.user.validation.NotBlank_,  _UserModule.entities.user.validation.alreadyExists.username_|
| *EntityPrefix*.adminMenu.general| Name of the _General_ tab.  Usually the first tab that is also opened when creating a new entity.|
| *EntityPrefix*.adminMenu.*associationName*| Name of the tab for that association. <br>Example: _UserModule.entities.group.adminMenu.user.groups_|
| *EntityPrefix*.actions.*actionName*| Name of the actions, usually the buttons or links on a page.  Often you just want to replace these on a global level. <br>Example: _EntityModule.entities.actions.save_, _UserModule.entities.group.actions.cancel_|
| *EntityPrefix*.pageTitle.*pageName*| Title of the page.  Supports message code parameters. <br>Example: _UserModule.entities.user.pageTitle.update=Updating {1}: {2}_|
| *EntityPrefix*.pageTitle.*pageName*.subText| Additional text that should be added as sub text (small) to the page header. Supports message code parameters.|
| *EntityPrefix*.feedback.*feedbackType*| Feedback message shown for the given feedback type. <br>Example: _UserModule.entities.user.feedback.validationErrors_|
| *EntityPrefix*.sortableTable.*| Sortable table results and pager text keys. <br>Example: _UserModule.entities.user.sortableTable.resultsFound_|
| *EntityPrefix*.delete.*| Delete view specific messages.<br>Example: _UserModule.entities.user.delete.confirmation_|

> _Entity_ codes are camel cased, eg. `CarBrand` would become *carBrand*

## EntityPrefix
Every code requested results in several codes being tried with a number of prefixes:
The following prefixes are tried in oder:

1. (If association view) _ModuleName_.entities._sourceEntityName_.associations[_associationName_]
2. _ModuleName_.entities._entityName_
3. EntityModule.entities._entityName_
4. EntityModule.entities

When rendering a view, the default prefix will be appended with a view type prefix as well.
Usually of the form _views[viewType]_.

Example lookup of property "name" on the default list view for entity "user":

1. MyModule.entities.user.views[listView].properties.name
2. MyModule.entities.user.properties.name
3. MyModule.entities.views[listView].properties.name
4. MyModule.entities.properties.name
3. EntityModule.entities.views[listView].properties.name
4. EntityModule.entities.properties.name

**TIP**: To get a better insight in the message codes generated, use the entity browser in the developer tools.

## Message code parameters
Some message codes support parameters, if so, the following could be available:

* {0}: entity name
* {1}: entity name inline
* {2}: label of the entity being modified (if known)

## Debugging message code lookups
You can trace the message codes being resolved by setting the logger named *com.foreach.across.modules.entity.support.EntityMessageCodeResolver* to _TRACE_ level.

## Default message codes
The following is a copy of **EntityModule.properties** which contains the default message codes for EntityModule.

```
# Default actions
EntityModule.entities.actions.create=Create a new {1}
EntityModule.entities.actions.view=View {1} details
EntityModule.entities.actions.update=Modify {1}
EntityModule.entities.actions.delete=Delete {1}
EntityModule.entities.actions.save=Save
EntityModule.entities.actions.cancel=Cancel

EntityModule.entities.menu.delete=Delete
EntityModule.entities.menu.advanced=Advanced options

EntityModule.entities.buttons.delete=Delete

EntityModule.entities.feedback.entityCreated=New {1} has been created.
EntityModule.entities.feedback.entityUpdated={0} has been updated.
EntityModule.entities.feedback.entityDeleted={0} has been deleted.
EntityModule.entities.feedback.entityDeleteFailed=Exception deleting {1}: {3}.
EntityModule.entities.feedback.validationErrors=Unable to save, please check the form for one or more errors.
EntityModule.entities.feedback.entitySaveFailed=Something went wrong when saving the {1}.  <br />Error code: <strong>{4}</strong> ({3}).

EntityModule.entities.pageTitle.create=Create a new {1}
EntityModule.entities.pageTitle.update=Modify {1}: {2}
EntityModule.entities.pageTitle.view=View {1} details: {2}
EntityModule.entities.pageTitle.delete=Delete {1}: {2}

EntityModule.entities.sortableTable.resultsFound={0,choice, 0#No {2}| 1#1 {1}| 1<{0} {2}} found.
EntityModule.entities.sortableTable.pager=Showing page {0,number,#} of {1,number,#}
EntityModule.entities.sortableTable.pager.page=page
EntityModule.entities.sortableTable.pager.ofPages=of
EntityModule.entities.sortableTable.pager.nextPage=next page
EntityModule.entities.sortableTable.pager.previousPage=previous page

EntityModule.entities.delete.confirmation=Are you sure you want to delete this {1} and all its associations?
EntityModule.entities.delete.deleteDisabled=Not possible to delete this {1}.
EntityModule.entities.delete.associations=The following items are associated with this {1}:
EntityModule.entities.delete.associatedResults={2} {1}

#
# Default validation messages
#
EntityModule.entities.validation.Size=Length should be between {2} and {1} characters.
EntityModule.entities.validation.Length=Length should be between {2} and {1} characters.
EntityModule.entities.validation.NotBlank=A value is required.
EntityModule.entities.validation.NotNull=A value is required.
EntityModule.entities.validation.NotEmpty=A value is required.
EntityModule.entities.validation.Email=Email address is not well-formed.
EntityModule.entities.validation.Min=Value should be greater than or equal to {1}.
EntityModule.entities.validation.Max=Value should be less than or equal to {1}.

EntityModule.entities.validation.alreadyExists=Another entity already has this value.

# Default control messages
BootstrapUiModule.SelectFormElementConfiguration.noneSelectedText=
```
