<a name="understanding-the-azure-portal-architecture"></a>
## Understanding the Azure Portal Architecture

The [Azure portal](http://portal.azure.com) is a [single page application](http://en.wikipedia.org/wiki/Single-page_application) which can dynamically load a collection of extensions. Extensions are simply web applications written using the Azure Portal SDK. These extensions are loaded in the azure portal via an IFrame. This allows extensions to load content securely in a isloated context.

The IFRAMEs loaded by the portal are entirely hidden. The scripts loaded by these IFRAME interact with the portal using Azure Portal SDK APIs. Using the Azure portal SDK APis allows the extensions to provide a consistent, and predictable experience for Azure portal users.

When a user visits the Azure portal, extensions will be loaded based on the users subscription. Extensions can be loaded asynchronously, and even deactivated when they are not currently in use.

**Azure portal architecture block diagram**

[Portal extension architecture](../media/portalfx-deployment/deployment.png)

<a name="understanding-the-azure-portal-extension-architecture"></a>
## Understanding the Azure Portal Extension Architecture

1. Typically an extension is an [ASP.NET Web API](http://www.asp.net/web-api) project, which is modified to include content specific to the portal.
1. The client APIs use [TypeScript](http://www.typescriptlang.org/) to provide a productive experience for building JavaScript.
1. TypeScript is built using the [Asynchronous Module Loader (AMD)](http://requirejs.org/docs/whyamd.html) module system via [require.js](http://requirejs.org/).
1. The core programming model follows the [Model View ViewModel](http://en.wikipedia.org/wiki/Model_View_ViewModel) pattern. Most [UI elements](portalfx-ui-concepts.md) in the portal are backed by dynamic view models, which provide a 'live tile' style of UX.
1. View models make heavy use of [Knockout](http://knockoutjs.com/) for binding data to the client.
1. Building custom UI is enabled using standard web technologies like [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) and [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS).
1. Extension developers can provide customers of your service consistent experience across all clients i.e. UI, powershell or CLI by implementing business logic in APIs exposed through ARM.
1. Azure portal mints tokens on behalf of extensions. This allows extensions to invoke ARM APIs out of the box. In case your extension needs to invoke services such as Graph then we recommend you go through [Authentication guide](portalfx-authentication.md) asap to check if you need help from our team.
1. Extension developers can leverage the extension hosting service to deploy extension's UI in all Azure data centers.



