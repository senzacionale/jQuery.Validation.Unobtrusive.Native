jQuery Validation Unobtrusive Native 
====================================

This is copy of https://github.com/johnnyreilly/jQuery.Validation.Unobtrusive.Native with some improvements and modifications for external libraries such as https://github.com/jwaliszko/ExpressiveAnnotations

jQuery.Validation.Unobtrusive.Native is a collection of ASP.Net MVC HTML helper extensions that make use of jQuery Validation's native unobtrusive support for validation driven by HTML 5 data attributes.  Microsoft shipped [jquery.validate.unobtrusive.js](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) back with MVC 3.  It provided a way to apply data model validations to the client side using a combination of jQuery Validation and HTML 5 data attributes (that's the "unobtrusive" part).

The principal of this was and is fantastic.  But since that time the jQuery Validation project has implemented its own support for driving validation unobtrusively (this shipped with [jQuery Validation 1.11.0](http://jquery.bassistance.de/validate/changelog.txt)).  The advantages of the native support over jquery.validate.unobtrusive.js are:

* Dynamically created form elements are parsed automatically.  jquery.validate.unobtrusive.js does not support this.
* jquery.validate.unobtrusive.js restricts how you use jQuery Validation.  Want to use showErrors etc?  Well you'll need to go native... 
* Send less code to your browser, make your browser to do less work, get a performance benefit (though you'd probably have to be the Flash to actually notice the difference)

This project intends to be a bridge between MVC's inbuilt support for driving validation from data attributes and jQuery Validation's native support for the same.  This is achieved by hooking into the MVC data attribute creation mechanism and using it to generate the data attributes used by jQuery Validation.

You can see more detail on the [demo site](http://johnnyreilly.github.io/jQuery.Validation.Unobtrusive.Native/).

##Getting started

If you haven't already, ensure that the following entries can be found in your web.config:

    <appSettings>
        <add key="ClientValidationEnabled" value="true" />
        <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    </appSettings>

Include jQuery.Validation.Unobtrusive.Native into your project (available on [nuget](http://www.nuget.org/packages?q=jQuery.Validation.Unobtrusive.Native) or on [GitHub](http://github.com/johnnyreilly/jQuery.Validation.Unobtrusive.Native)). With this in place you should be able to switch from using the existing `TextBoxFor` / `DropDownListFor` / `CheckBoxFor` / `TextAreaFor` / `RadioButtonFor` / `ListBoxFor` / `PasswordFor` HtmlHelper statements in your views and to jQuery.Validation.Unobtrusive.Native's equivalent by passing `true` to the `useNativeUnobtrusiveAttributes` parameter. (By convention this is the first parameter after the `Expression<Func<TModel, TProperty>> expression` parameter.
	
Ensure that you have the latest version of jquery.validate.js, you can find it [here](http://jqueryvalidation.org/).  Oh, and remember that you *no longer* need to serve up the jquery.validate.unobtrusive.js on a screen where you are using jQuery.Validation.Unobtrusive.Native.  All you need is jquery.validate.js (and of course jQuery).

P.S. If you're using the source code from GitHub in Visual Studio, make sure you have the Package Manager option *"Allow NuGet to download missing packages during build"* set to true.  This will ensure that the required packages are downloaded from NuGet.

##Examples

Where you would previously have written:

    @Html.TextBoxFor(x => x.RangeAndNumberDemo)

To use jQuery.Validation.Unobtrusive.Native you would put:

    @Html.TextBoxFor(x => x.RangeAndNumberDemo, true)

Or, where you would have written:

    @Html.DropDownListFor(x => x.DropDownRequiredDemo, new List<SelectListItem> {
        new SelectListItem{ Text = "Please select", Value = "" },
        new SelectListItem{ Text = "An option", Value = "An option"}
    })

Now you would put:

    @Html.DropDownListFor(x => x.DropDownRequiredDemo, true, new List<SelectListItem> {
        new SelectListItem{ Text = "Please select", Value = "" },
        new SelectListItem{ Text = "An option", Value = "An option"}
    })

The only differences above are the extra `true` parameters being passed.  If you had passed `false` instead jQuery.Validation.Unobtrusive.Native internally calls the inbuilt MVC implementation.  I have considered keeping jQuery.Validation.Unobtrusive.Native's HtmlHelpers entirely separate from the inbuilt MVC ones and instead implementing `TextBoxNativeFor` / `DropDownListNativeFor` etc... methods which share the same signatures as the inbuilt MVC ones.  For now this is the way it is but it could change if people feel strongly enough - if you've an opinion then drop me a line with your rationale.

By the way, the above examples (and others) can be found in the MVC demo project jVUNDemo on GitHub - this demo site be viewed at [johnnyreilly.github.io/jQuery.Validation.Unobtrusive.Native/](http://johnnyreilly.github.io/jQuery.Validation.Unobtrusive.Native/).  2 of the demos ([Remote](http://johnnyreilly.github.io/jQuery.Validation.Unobtrusive.Native/Demo/Remote.html) and [Globalize](http://johnnyreilly.github.io/jQuery.Validation.Unobtrusive.Native/AdvancedDemo/Globalize.html)) do not work completely as static sites (which GitHub pages are).  If you would like to see these demo's in action it's best you run the jVUNDemo project locally.

## Author
**John Reilly**

+ http://twitter.com/johnny_reilly

**Mija Bombac**

## Credits
Inspired by jquery.validate.unobtrusive.js and entirely dependent on http://github.com/jzaefferer/jquery-validation and http://aspnet.codeplex.com/wikipage?title=MVC.

## Copyright
* Copyright � 2013 [John Reilly](mailto:johnny_reilly@hotmail.com).
* Copyright � 2015 [Mitja Bombac]

##License

MIT license - [http://www.opensource.org/licenses/mit-license.php](http://www.opensource.org/licenses/mit-license.php)