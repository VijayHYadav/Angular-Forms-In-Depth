
## ControlValueAccessor

If we want to take a custom component and have it integrate well with the Angular Forms library, we need to have it implement the control value accessor interface.

This is what is going to allow us to apply the form Control Directive into that component or even use the Ng-model directive that would work well to the control value accessor is made of these four methods.These are meant to be called by the angular forms module only, and we are not supposed to call these methods ourselves.

interface ControlValueAccessor {
  writeValue(obj: any): void
  registerOnChange(fn: any): void
  registerOnTouched(fn: any): void
  setDisabledState(isDisabled: boolean)?: void
}

Notice that in order for the component to be fully integrated with angular forms, we are also going to have to implement a second interface, which is the validator interface.

The first and most important one is the right value method. These methods, just like all the form method of the control value interface, is not meant to be called by as manually inside our component. These four methods are meant to be called by the angular forms module only.So if you see code where these methods are being called manually, that is probably a error.


So when are each of these four methods called by the angular forms module?
In order to understand each of these methods, let's remember that our custom form control, our file upload component is going to be part of form.
So that form is going to want to set values for each of its properties and the form will also want to be notified whenever some of those property changes.

So the form is responsible for gathering the value of each individual property.
If, for example, we will initialize our form with an initial value, then the form needs a way of setting the value of each of its individual properties.
Each form property is going to have a control value accessor associated to it.
The association is made by directives that are part of the angular forms module. Some are built in and some are custom like the case of our file upload component.
So each property has a control value accessor.So whenever the form needs to set the value of a given property, it can do so by calling the right value method. Once the value of the form is set, then the user is going to start to interact with the form and the user will input new values.

The form also wants to get notified when a new value is available and the forum can get that notification by registering(registerOnChange) here a callback.
So the form is going to contact each of the control value accessors of its properties and it's going to register on change on it at form initialization time.
Then when the form property changes because the user has typed in a new value, for example, this unchanged callback is going to get called and the form is going to get notified of the new value for that particular property.

In a very similar way. The form also wants to know whenever a form of control was touch. By the user, whenever a single control in the form gets touch by the user, then the whole the state of the whole form is going to be set to true.

And finally, the form can also set and enabled or disabled state for each of its child properties. So each child property of the form has a control value accessor associated to it, and the form can set the state of its control by calling set disabled states.

However, in the case of other controls in our form, such as for example, in normal inputs, dropdown, checkboxes, etc., those components already have a built in control value accessor implementation, which is part of the angular forms module.