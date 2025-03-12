# Naming conventions


Following the naming conventions is important to ensure there is consistency across the code and ease of readability. Obviously, it's impossible to have everyone think alike, but if we follow the following vectors we should be able to achieve a lot more consistent namings. 

As a thumb rule always follow:
_PascalCasing_ for any OutSystems elements/objects/actions/list/table/etc
_camelCasing_ in JS, its variables.
_hyphenated-lower-case-class-name_ for css classes.


## **Actions**

Page/Block event: OnReady (prefix with On plus lifecycle event)
ScreenAction:
DataActionEvents: _OnAfterFetchGetClaimDetailById_ (prefix with OnAfterFetch plus data action name)
HTML event: _OnChangePaymentMethod_ (Prefix with On plus html event plus widget name)
Event Trigger: _EventAddExpense_ (Prefix with Event plus Action starting with the verb)
EventHander: _EventHandlerAddExpense_ (Prefix with EventHandler plus Action starting with the verb)
Local client actions: _LocalScrollIntoView_ (Prefix with local plus action name)

## **Variable/entity attributes**

Boolean:  _IsSaved/HasAcceptedTermsAndConditions_ (Prefix with verb)
Date:  _ExpenseDate_ (Suffix with Date)
Identifiers: _ClaimId_ (Suffix with Id )

## **Widgets**

As a best practice and to ensure unique locator availability for automation testing purposes, we will need to set meaningful names to the elements.

OutSystems names elements by default in most cases, we will utilize the same but adding with the element field related to. 

**Block_<Element><Label>**

Here, **BlockName** will not be necessary in most situations.
So, a combo of <Element><Label> is enough. ex: **InputClaimAmount**

**<Label>** is not always obvious, it could be a radio options value or a shortened purpose of a widget, like **CheckboxAgreeSAGovDeclaration**

**BlockName** needed as a prefix when 2 different blocks is having same name field which could end up on the same page.
ex:
BpayVendors_InputVendorName
BankVendors_InputVendorName


**<u>Below are different elements naming examples</u>**:
- InputFirstName
- InputSearchTransactions
- InputDateOfTaxInvoice
- InputBankAccountBSB
- TextAreaClaimDescription
- Contact_TextAreaComment
- CheckboxUploadedForms
- RadioGroupClaimsType
- RadioButtonReimbursement
- SwitchMarketingEmails
- DropdownVehicleRego
- UploadClaimsReciept
- LinkCancelClaim
- ButtonProceedToUpload
- Declaration_ButtonCancel
- WalletBalance_ButtonCancel


Note: There are other ways for testers to capture links, so where it get complicated you can avoid naming links, or try to name with their purpose.

The idea is to avoid identical ids getting generated of the same name and within the same page, it can be identical in different unrelated page blocks.

----------------------------------------------------------------- For Testers Only-----------------------------------------------------------------

Below has detailed information on the usage, but consider above Naming conventions:

**Widget Naming**
The way automated UI testing works in applications is by simulating the user interaction through application screens in order to fulfill a specific user journey or functionality provided by the application. This simulation is done through scripting the various steps a user needs to perform on the screen elements. An example would be: Follow the home menu link; Click on the submit button; Enter the email@example.com into the email input.

This means that the UI script needs to uniquely identify the elements that the user is interacting with. The easiest way to uniquely identify an element in a screen is through its ID property. As such, and in the scope of OutSystems application screens, it implies that those widgets need to be properly identified in Service Studio.

When developing a screen, the developer should ensure that all elements that have some degree of user interaction, such as inputs, buttons, and links, have the name property assigned with a meaningful value. This facilitates the element identification in the generated screen code, since the element’s ID attribute will always terminate with the widget’s name property value. This will also avoid additional effort later on if a UI test finds that a specific element on the screen is not properly identified.

Eventually, it may be the case that a specific UI test will require additional elements on the screen, which will also need identifiers. However, by naming at least the widgets mentioned above, the developer minimizes the number of times that rework needs to be done. Saving some of this effort fosters a faster workflow when implementing UI testing.

Using the name as the basis of the selector also allows the platform to detect name collision inside the same screen. This is an added benefit. It does not allow two different widgets to have the same Name property, and so the second will add the suffix of "2", and so on.

Still, because OutSystems allows composing a screen with multiple Blocks, if we use the same name in two different Blocks for the same screen, this name collision will not be automatically addressed by Service Studio. Taking that into account, we recommend that when naming a widget in a block, developers should include the block name as a prefix to the name of the UI widget. This ensures that names will still be unique when a screen is composed by multiple, different Blocks.

And what if there is a need to have multiple instances of the same block on the same screen? In these scenarios, developers should wrap each block in a container with a specific ID for the screen, and then use that container ID to anchor each specific block instance in a unique way for that screen.

Testing tools usually use XPath or CSS selectors to identify each UI element. When following the approach mentioned above for UI element identification, these UI widgets will all have IDs, but the OutSystems platform will generate a "composed" ID that will only end with the actual name given to the widget inside Service Studio.

The following is a simple example of how you can identify these IDs that end with a given unique name. Remember, the name represents both CSS selectors and XPath selectors for an input with the name "UserNameInput" in Service Studio:

CSS Selector
input[id$=UserNameInput]
XPath Selector (1.0)
//input[substring(@id, string-length(@id) - string-length('UserNameInput') + 1) = 'UserNameInput']
XPath Selector (2.0) not commonly supported by testing tools
//input[ends-with(@id,’UserNameInput’)]