# A taste from the eXpandFramework/DevExpress.XAF Github repository

Why only the standalone packages?

These packages are Test Driven Developed, a technique that leads to a robust well documented code with a long life cycle.
The DevExpress.XAF repository contains a great number of XAF modules, tools and libraries aim to enhance our everyday work and applications. 

First **Credits** go to the hidden yet indispensable player the `CI/CD`, which `automates everything`that can be automated using the [XpandPwsh](https://github.com/eXpandFramework/XpandPwsh) `powershell` module in the `Azure DevOps` environment. It provides consistent endpoints that we can use to address our tasks. For example it publishes the Nuget packages in a consistent way, it runs the unit and EasyTest we have against different environment, it checks project files inconsistencies, it updates documentation parts and much more tasks that help `increase` the `trust level` we have to the resulted published `packages`.

As the `CI/CD` is the `major player` in a project life cycle, we `weight more the tools` that make it happen than the actual modules that almost everybody can write. However the the emphasis must be on `how long` can they stay `alive` so they work for us and not for them. 

1. The three container nuget packages [Xpand.XAF.Core.All](https://www.nuget.org/packages/Xpand.XAF.Core.All), [Xpand.XAF.Win.All](https://www.nuget.org/packages/Xpand.XAF.Win.All), [Xpand.XAF.Web.All](https://www.nuget.org/packages/Xpand.XAF.Web.All) will bring all packages at your disposal in a lazy manner. Meaning all API is available in the VS intellisense however if not used the assembly with not be a dependency. Therefore they `zeroing` the `efforts` to install the packages explicitly and handle their `version conflicts`. In addition they provide the required installation `installation snippets`.</br>
In the next screencast we see how easy is to install all packages that target the Windows platform. It is recommended to use the Nuget `PackageReference` format. First we install all packages and make a note that a dependency is added for all, then we remove a few installation lines and we make a note how the assembly dependencies reflects only that used API. The assembly reference discovery was done with the help of the XpandPwsh [Get-AssemblyReference](https://github.com/eXpandFramework/XpandPwsh/wiki/Get-AssemblyReference) cmdlet.</br>
![Xpand XAF All](https://user-images.githubusercontent.com/159464/86915211-447c3780-c12a-11ea-973d-3096044dc22b.gif)

    ---

1. The cross platform [Xpand.VersionConverter](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/tools/Xpand.VersionConverter) package contains `MSBuild targets` and `Powershell` scripts that provide assembly `compatibility` through `XAF versions` without the need to recompile therefore takes away a large support cost. `All` standalone packages already `use` the `Xpand.VersionConverter` and also is possible to configure to work for your Company namespace instead of Xpand that works by default.</br>
The `Xpand.VersionConverter` package makes it possible to run our `tests against multiple XAF versions `and produce really valuable `compatibility matrixes` like:
    |![Custom badge](https://xpandshields.azurewebsites.net/endpoint?style=plastic&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FXAFBuild%3Findex%3D1%26branch%3Dmaster%26shield%3Dcoverage)| Release  | Lab|
    |---|---|---|
    |![Custom badge](https://xpandshields.azurewebsites.net/endpoint?style=for-the-badge&label=%20&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FLatestXAFMinors%3Findex%3D1)|![Custom badge](https://xpandshields.azurewebsites.net/endpoint?style=plastic&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FXAFBuild%3Findex%3D1%26branch%3Dmaster%26shield%3Dtests)|![Custom badge](https://xpandshields.azurewebsites.net/endpoint?&style=plastic&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FXAFBuild%3Findex%3D1%26branch%3Dlab%26shield%3Dtests)
    |![Custom badge](https://xpandshields.azurewebsites.net/endpoint?label=%20&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FLatestXAFMinors%3Findex%3D2)|![Custom badge](https://xpandshields.azurewebsites.net/endpoint?style=plastic&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FXAFBuild%3Findex%3D2%26branch%3Dmaster%26shield%3Dtests)|![Custom badge](https://xpandshields.azurewebsites.net/endpoint?style=plastic&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FXAFBuild%3Findex%3D2%26branch%3Dlab%26shield%3Dtests)
    |![Custom badge](https://xpandshields.azurewebsites.net/endpoint?label=%20&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FLatestXAFMinors%3Findex%3D3)|![Custom badge](https://xpandshields.azurewebsites.net/endpoint?style=plastic&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FXAFBuild%3Findex%3D3%26branch%3Dmaster%26shield%3Dtests)|![Custom badge](https://xpandshields.azurewebsites.net/endpoint?style=plastic&url=https%3A%2F%2Fxpandnugetstats.azurewebsites.net%2Fapi%2Ftotals%2FXAFBuild%3Findex%3D3%26branch%3Dlab%26shield%3Dtests)

    In the screencast you can see how to make `Xpand.VersionConverter` extend the lifetime of your Company packages.

    ---

1. The cross platform [Xpand.XAF.Modules.SequenceGenerator](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/SequenceGenerator) generates unique sequential values and provides a XAF UI so the end user can link those values to Business objects members.</br>
    In the next screencast we use the XAF UI to create a `subscription` to the `sequence` generator and `assign` the generated sequence to our  `Order.OrderId` configuring the initial sequence to `1000`. Similarly for `Accessory.AccessoryId` where we set the initial value to `2000`. Finally we test by creating an Order and an Accessory where we can `observe` the assigned `values` of OrderId, AccessoryId.

    [![hfvTo7UsCI](https://user-images.githubusercontent.com/159464/80309035-f918e500-87da-11ea-8f52-7799457213cf.gif)](https://www.youtube.com/watch?v=t1BDPFU01z8)

    ---

1. The cross platform [Xpand.XAF.Modules.ModelMapper](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/ModelMapper) module can `convert` any `Type` to XAF application `model` extension and and at `runtime map` them back to the related object instances. Ships with `predefined maps` for `all` the common XAF `components` such as Grids, Charts, Tree, Pivot etc.</br>
In the next screencast we see how to extend the `IModelListView` with the `GridView` component and the `IModelColumn` with the `GridColumn` component. Then we `false` `Customer.FirstName` using the `IModelColumn.GridColumn.OptionsColumn.AllowSort` model attribute and we test using the XAF UI that the Customer.FirstName is not sortable anymore.</br></br>

   ![aYbdUf4HwV](https://user-images.githubusercontent.com/159464/86943203-d1d18300-c14e-11ea-9d68-ee68ff57455f.gif)

    ---

1. The cross platform [Xpand.XAF.Modules.ModuleViewInheritance](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/ModelViewInheritance) module `reprograms` the default `design-time` model `view generation` to respect existing view model differences.</br>
 In the next screencast: 
   1. We used the [CloneView](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/CloneModelView) package to clone the `BaseObject_ListView` as a `CommonGridView_ListView`. We prefer this the CloneView package as it does not pollute the model with differences. In addition since the `BaseObject` type lives in an assembly we do not own we declare the CloneViewModelAttribute dynamically by extending the XAF typesinfo system.
   2. Next, the [Xpand.XAF.Modules.Reactive](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/Reactive) `WhenGeneratingModelNodes` is used to assign the `CommonGridView_ListView` as a `base` view.
   3. Next we extend the model with the GridView component using the [Xpand.XAF.Modules.ModelMapper](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/ModelMapper)
   2. Finally, we `modify` the CopyToClipBoard value on the `CommonGridView_ListView` and `check` that is reflected appropriately on the `Customer_ListView`. </br></br>
   
   ![jiRSdwmukl](https://user-images.githubusercontent.com/159464/86963022-84640e80-c16c-11ea-8f8d-523a4d6f3312.gif)

   ---

1. The cross platform [Xpand.XAF.Modules.Office.Cloud.Microsoft](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/Office.Cloud.Microsoft) authenticates against Azure Active Directory and provides API for querying the MSGraph endpoints. Related packages that use it and pending release are the `Xpand.XAF.Modules.Office.Cloud.Microsoft.Todo` and `Xpand.XAF.Modules.Office.Cloud.Microsoft.Calendar`</br>
Below is a demonstration of the package authenticating against `ADD` for both `Win/Web`. Also the API is used to call the `MSGraph` [Me](https://docs.microsoft.com/en-us/graph/api/user-get?view=graph-rest-1.0&tabs=http) endpoint for displaying the authenticated user info in a XAF view. At the bottom the [Reactive.Logger.Client.Win](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/Reactive.Logger.Client.Win) is reporting as the module is used. This demo it is Easytested [with this script](https://github.com/eXpandFramework/DevExpress.XAF/blob/master/src/Tests/ALL/CommonFiles/MicrosoftService.cs) for the last three XAF major versions, compliments of the `Xpand.VersionConverter` as described in #2</br></br>

   [![Xpand XAF Modules Office Cloud Microsoft](https://user-images.githubusercontent.com/159464/86131887-e24e8180-baee-11ea-8c02-b64b2c639b6d.gif)](https://www.youtube.com/watch?v=XIczKjE2sFw)

For more examples and details navigate the `eXpandFramework/DevExpress.XAF` [wiki]()
