---
-api-id: T:Windows.UI.WebUI.WebUIContactMessageActivatedEventArgs
-api-type: winrt class
---

<!-- Class syntax.
public class WebUIContactMessageActivatedEventArgs : Windows.ApplicationModel.Activation.IActivatedEventArgs, Windows.ApplicationModel.Activation.IContactActivatedEventArgs, Windows.ApplicationModel.Activation.IContactMessageActivatedEventArgs, Windows.UI.WebUI.IActivatedEventArgsDeferral
-->

# Windows.UI.WebUI.WebUIContactMessageActivatedEventArgs

## -description
Provides data when an app is activated to message a contact.

## -remarks
This object is accessed when you implement an event handler for the [WinJS.Application.Onactivated](http://msdn.microsoft.com/library/8b1cf913-a914-47d1-a690-bc3f0931e9d4) or the [Windows.UI.WebUI.WebUIApplication.activated](webuiapplication_activated.md) events when [ActivationKind](../windows.applicationmodel.activation/activationkind.md) is **contact**.



> [!NOTE]
> : This class is not agile, which means that you need to consider its threading model and marshaling behavior. For more info, see [Threading and Marshaling (C++/CX)](http://go.microsoft.com/fwlink/p/?linkid=258275).

Windows 8.1 allows users to message their contacts from the [Contact Card](../windows.applicationmodel.contacts/contactmanager_showcontactcard_1968125937.md) or Windows Search experience. By implementing the contact message activation contract, Windows can launch your app to send messages for the user.

To receive message activations, your app must register for the "windows.contact" extension category in its manifest. Under this extension, you must include a "LaunchAction" element with the "Verb" attribute equal to "message." You can then specify the "ServiceId" element to specify the type of messaging you support. For example, if your app handles standard text messages, you can specify a "ServiceId" of "telephone." If your app handles messaging over a web based service, like Skype, you can specify the domain name of that service, for example "skype.com."

If multiple apps have registered for this contract, the user can choose one of them as their default for handling messages.



Here is an example for manifest registration:

```xml

<m2:Extension Category="windows.contact" xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest">
  <m2:Contact>
    <m2:ContactLaunchActions>
      <m2:LaunchAction Verb="message" DesiredView="useLess">
        <m2:ServiceId>telephone</m2:ServiceId>
      </m2:LaunchAction>
      <m2:LaunchAction Verb="message" DesiredView="useLess">
        <m2:ServiceId>skype.com</m2:ServiceId>
      </m2:LaunchAction>
    </m2:ContactLaunchActions>
  </m2:Contact>
</m2:Extension>

```



After you register in your manifest, your app can be activated for the contact message contract. When your app is activated, you can use the event information to identify the message activation and extract the parameters that help you complete the messaging scenario for the user.

Here is an example of the code you need to handle contact message activations for PSTN numbers and Skype Ids:

## -examples
JavaScript

```javascript
function activated(eventObject) {
    if (eventObject.detail.kind === Windows.ApplicationModel.Activation.ActivationKind.contact) {
        if (eventObject.detail.verb === Windows.ApplicationModel.Contacts.ContactLaunchActionVerbs.message) {

     //get contact display info
            var contactName = eventObject.detail.contact.displayName;
            var contactThumbnail = eventObject.detail.contact.thumbnail;

            if (eventObject.detail.serviceId === "telephone") {
                var phoneNumber = eventObject.detail.serviceUserId;
  //add messaging logic for PSTN numbers
            }
     else if (eventObject.detail.serviceId === "skype.com") {
                var userId = eventObject.detail.serviceUserId;
  //add messaging logic for Skype Ids
            }
        }
    }
}

```



## -see-also
[IContactMessageActivatedEventArgs](../windows.applicationmodel.activation/icontactmessageactivatedeventargs.md), [IContactActivatedEventArgs](../windows.applicationmodel.activation/icontactactivatedeventargs.md), [IActivatedEventArgs](../windows.applicationmodel.activation/iactivatedeventargs.md), [IActivatedEventArgsDeferral](iactivatedeventargsdeferral.md), [Handling Contact Actions sample](http://go.microsoft.com/fwlink/p/?LinkID=320151)