---
-api-id: T:Windows.ApplicationModel.Activation.LaunchActivatedEventArgs
-api-type: winrt class
---

<!-- Class syntax.
public class LaunchActivatedEventArgs : Windows.ApplicationModel.Activation.IActivatedEventArgs, Windows.ApplicationModel.Activation.IActivatedEventArgsWithUser, Windows.ApplicationModel.Activation.IApplicationViewActivatedEventArgs, Windows.ApplicationModel.Activation.ILaunchActivatedEventArgs, Windows.ApplicationModel.Activation.ILaunchActivatedEventArgs2, Windows.ApplicationModel.Activation.IPrelaunchActivatedEventArgs, Windows.ApplicationModel.Activation.IViewSwitcherProvider
-->

# Windows.ApplicationModel.Activation.LaunchActivatedEventArgs

## -description
Provides event information when an app is launched.

> **JavaScript**
> This type appears as [WebUILaunchActivatedEventArgs](../windows.ui.webui/webuilaunchactivatedeventargs.md).

## -remarks
This object is accessed when you respond to [Activated](../windows.applicationmodel.core/coreapplicationview_activated.md) events when [ActivationKind](activationkind.md) is **Launch**.

UWP app using C++, C#, or Visual Basic typically implement activation points by overriding methods of the [Application](../windows.ui.xaml/application.md) object. The default template app.xaml code-behind files always include an override for [OnLaunched](../windows.ui.xaml/application_onlaunched_859642554.md). The default implementation includes initial navigation support and state management through the SuspensionManager helper class.

All [Application](../windows.ui.xaml/application.md) overrides involved in an activation scenario should call [Window.Activate](../windows.ui.xaml/window_activate_1797342875.md) in their implementations.

Avoid performing tasks during launch if they could significantly increase the time required to launch your app. Instead, you can trigger additional loading tasks by listening for the [SplashScreen.Dismissed](splashscreen_dismissed.md) event.

The activation deferral object should not be used to complete complex tasks during activation. Any unhandled errors or exceptions that occur during activation (including deferred activation) will cause the app to crash. If you need to perform network calls or process a number of additional files during activation, consider launching your app to an extended splash screen and then performing these operations. For more information, see [How to display a splash screen for an extended time](http://msdn.microsoft.com/library/fd10a9ff-4e09-471f-886e-8b8246dc12de).

> [!IMPORTANT]
> Apps that require an excessive amount of time to launch may be terminated by the system.

When testing your app, be aware that immediately reactivating an app that has just been terminated will result in a failed activation if the splash screen is still visible.

### JavaScript launch completion

If programming with JavaScript, launch is complete when your activated event handler returns successfully after executing your launch tasks. 


### .NET launch completion

If programming with C#, VB, or C++, launch is complete when you activate an app window. 


## -examples

## -see-also
[Handle app activation](http://msdn.microsoft.com/library/da9a6a43-f09d-4512-a2ab-9b6132431007), [Windows.UI.Core.CoreApplicationView.Activated](../windows.applicationmodel.core/coreapplicationview_activated.md), [Application](../windows.ui.xaml/application.md), [OnLaunched](../windows.ui.xaml/application_onlaunched_859642554.md)