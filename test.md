# Problem solutions from the eXpandFramework/DevExpress.XAF Github repository
1. **Due to the large package number a substantial effort is needed even for simple tasks, like installation, package API discovery and version choosing. How to get the best out of them?**

   </br><u>Solution:</u>
    Use `only` the `three` container nuget packages [Xpand.XAF.Core.All](https://www.nuget.org/packages/Xpand.XAF.Core.All), [Xpand.XAF.Win.All](https://www.nuget.org/packages/Xpand.XAF.Win.All), [Xpand.XAF.Web.All](https://www.nuget.org/packages/Xpand.XAF.Web.All). They come with the next benefits:
    * `All` packages `API` is available in the VS intellisense as soon as you start typing. 
    * You do `not` have to deal with versions `conflict`.
    * You will get a `copy-paste` module `registration` snippet. 
    * No extra dependencies if package API is not used.

    </br>In the next screencast we see how easy is to install all packages that target the Windows platform. It is recommended to use the Nuget `PackageReference` format. First we install all packages and make a note that a dependency is added for all, then we remove a few installation lines and we make a note how the assembly dependencies reflects only that used API. The assembly reference discovery was done with the help of the XpandPwsh [Get-AssemblyReference](https://github.com/eXpandFramework/XpandPwsh/wiki/Get-AssemblyReference) cmdlet.</br>
    ![Xpand XAF All](https://user-images.githubusercontent.com/159464/86915211-447c3780-c12a-11ea-973d-3096044dc22b.gif)

    ---

1. **We have a lot of XAF packages compiled against previous XAF versions.  How to reuse them in the latest version without recompilation?**

    </br><u>Solution:</u>
    Use the [Xpand.VersionConverter](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/tools/Xpand.VersionConverter) to patch your packages on the fly in relation to the consuming project skipping the need for a complex CI/CD.

    </br>In the screencast you can see how to make `Xpand.VersionConverter` extend the lifetime of your Company packages.

    ---

1. **Our Invoices and Orders must use unique sequential values in a multi user environment. How can we do it?**
    </br><u>Solution:</u>
    The cross platform [Xpand.XAF.Modules.SequenceGenerator](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/SequenceGenerator) generates unique sequential values and provides a XAF UI so the end user can link those values to Business objects members.</br>

    </br>In the next screencast we use the XAF UI to create a `subscription` to the `sequence` generator and `assign` the generated sequence to our  `Order.OrderId` configuring the initial sequence to `1000`. Similarly for `Accessory.AccessoryId` where we set the initial value to `2000`. Finally we test by creating an Order and an Accessory where we can `observe` the assigned `values` of OrderId, AccessoryId.

    [![hfvTo7UsCI](https://user-images.githubusercontent.com/159464/80309035-f918e500-87da-11ea-8f52-7799457213cf.gif)](https://www.youtube.com/watch?v=t1BDPFU01z8)

        ---

1. **We want to give our power users control over all major components used from XAF through Model Editor**
</br><u>Solution:</u>
The cross platform [Xpand.XAF.Modules.ModelMapper](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/ModelMapper) ships with `predefined maps` for `all` the common XAF `components` such as Grids, Charts, Tree, Pivot etc.
</br>In the next screencast we see how to extend the XAF model with the `GridView` and the `GridColumn` components. Then we used the model editor to modify the model and run the application to test our changes at runtime.</br></br>

   ![aYbdUf4HwV](https://user-images.githubusercontent.com/159464/86943203-d1d18300-c14e-11ea-9d68-ee68ff57455f.gif)

    ---

1. **We want to change the default Model View generation without coding, using the XAF ModelEditor**
</br><u>Solution:</u>
The cross platform [Xpand.XAF.Modules.ModuleViewInheritance](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/ModelViewInheritance) module `reprograms` the default `design-time` model `view generation` to respect existing view model differences.
 </br>In the next screencast: 
   1. First we extend the model with the GridView component using the [Xpand.XAF.Modules.ModelMapper](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/ModelMapper).
   1. Then, we used the [CloneView](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/CloneModelView) package to clone the `BaseObject_ListView` as a `CommonGridView_ListView`. 
   2. Next, the [Xpand.XAF.Modules.Reactive](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/Reactive) `WhenGeneratingModelNodes` is used to assign the `CommonGridView_ListView` as a `base` view.
   2. Finally, we `modify` the CopyToClipBoard value on the `CommonGridView_ListView` and `check` that is reflected appropriately on the `Customer_ListView`. </br></br>
   
   ![jiRSdwmukl](https://user-images.githubusercontent.com/159464/86963022-84640e80-c16c-11ea-8f8d-523a4d6f3312.gif)

   ---
1. **We want the end user to configure the default lookup values for certain views**
</br><u>Solution:</u>
Use the cross platform [Xpand.XAF.Modules.ViewItemValue](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/ViewItemValue)

   </br> In the screencast we configure the model to allow end user to choose the default values for `Product` and `Order` when he is on the `Order_DetailView`
   [![kMok40PDFn](https://user-images.githubusercontent.com/159464/83734915-4e58d980-a658-11ea-90db-c05fa9f614ac.gif)](https://www.youtube.com/watch?v=90MzTKyVlsg&t=21s)

1. **We want the end user to create persistent (through application restarts) configurations  on how objects are positioned in a ListView**
</br><u>Solution:</u>
Use the cross platform [Xpand.XAF.Modules.PositionInListView](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/PositionInListView)


   </br>In the screencast we create three customers at runtime and demo the feature by executing the MoveUp/MoveDown actions and close/reopen the view`. At the bottom the [Reactive.Logger.Client.Win](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/Reactive.Logger.Client.Win) is reporting as the module is used
   [![sqFoseHS2q](https://user-images.githubusercontent.com/159464/82759129-e4d50180-9df3-11ea-8bb9-eb6b36452c51.gif)](https://www.youtube.com/watch?v=JBoVNXo19ek)

1. **We want to create a persistent authentication against Azure Active Directory and integrate our apps with the MSGraph endpoints**
</br><u>Solution:</u>
Use the cross platform [Xpand.XAF.Modules.Office.Cloud.Microsoft](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/Office.Cloud.Microsoft) authenticates against Azure Active Directory and provides API for querying the MSGraph endpoints.</br>
Below is a demonstration of the package authenticating against `AAD` for both `Win/Web`. Also the API is used to call the `MSGraph` [Me](https://docs.microsoft.com/en-us/graph/api/user-get?view=graph-rest-1.0&tabs=http) endpoint for displaying the authenticated user info in a XAF view. At the bottom the [Reactive.Logger.Client.Win](https://github.com/eXpandFramework/DevExpress.XAF/tree/master/src/Modules/Reactive.Logger.Client.Win) is reporting as the module is used. This demo it is Easytested [with this script](https://github.com/eXpandFramework/DevExpress.XAF/blob/master/src/Tests/ALL/CommonFiles/MicrosoftService.cs) for the last three XAF major versions, compliments of the `Xpand.VersionConverter` as described in #2</br></br>

   [![Xpand XAF Modules Office Cloud Microsoft](https://user-images.githubusercontent.com/159464/86131887-e24e8180-baee-11ea-8c02-b64b2c639b6d.gif)](https://www.youtube.com/watch?v=XIczKjE2sFw)

For more examples and details navigate the `eXpandFramework/DevExpress.XAF` [wiki](https://github.com/eXpandFramework/DevExpress.XAF/wiki)
