# Get started with Azure API Management

This guide shows you how to quickly get started using API Management and make your first API call.

## In this topic

-	[Create an API Management instance][]
-	[Create an API][]
-	[Add an operation][]
-	[Add the new API to a product][]
-	[Subscribe to the product that contains the API][]
-	[Call an operation from the Developer Portal][]
-	[View analytics][]
-	[Next steps][]




## <a name="create-service-instance"> </a>Create an API Management instance

The first step in working with API Management is to create a service instance. Log in to the [Management Portal][] and click **New**, **App Services**, **API Management**, **Create**.

![api-management-create-instance-menu][]

For **URL**, specify a unique sub-domain name to use for the service URL.

Choose the desired **Pricing Tier**, **Subscription**, and **Region** for your service instance. All pricing tiers can be used for this tutorial. After making your selections, click the next button.

![api-management-create-instance-step1][]

Enter **Contoso Ltd.** for the **Organization Name**, and enter your email address in the administrator e-mail field.

>This email address is used for notifications and subscriptions approvals which are not covered in this tutorial but are covered in the following advanced tutorials. For more information, see [Next steps][].

Click the check box to create your service instance.

![api-management-create-instance-step2][]

After a few moments your service instance will be created.

![api-management-instance-created][]

Once the service instance is created, the next step is to create an API.

## <a name="create-api"> </a>Create an API

An API in API Management represents a set of operations that can be invoked by client applications. Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management. The Echo API returns back whatever input is sent to it. To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.

There are two parts to the Echo API:

-	The Echo API, operations, and policies that are configured in API Management
-	The Echo API back-end service hosted at http://echoapi.cloudapp.net/api

This tutorial uses the http://echoapi.cloudapp.net/api web service to create a new API in API Management called **My Echo Service**.

APIs are created and configured from the API Management portal, which is access through the Azure management portal. To reach the API Management portal, click **Management Console** in the Azure Portal for your API Management service.

![api-management-management-console][]

To create the **My Echo API**, click **APIs** from the **API Management** menu on the left, and then click **add API**.

![api-management-create-api][]

![api-management-add-new-api][]

The following three fields are used to configure the new API.

-	Type **My Echo API** into the **Web API Title** textbox. **Web API Title** provides a unique and descriptive name for the API. It is displayed in the developer and management portals.
-	Type **http://echoapi.cloudapp.net/api** into the **Web service URL**. **Web service URL** references the HTTP service implementing the API. API management forwards requests to this address.
-	Type **myecho** into the **Web API URL suffix**. **Web API URL suffix** is appended to the base URL for the API management service. Your APIs will share a common base URL and be distinguished by a unique suffix appended after the base.

Click **Save** to create the API. Once the new API is created, the summary page for the API is displayed in the management portal.

![api-management-new-api-summary][]

The API section has four tabs. The **Summary** tab display basic metrics and information about the API. The **Settings** tab is used to view and edit the configuration for an API, including authentication credentials for the back-end service. The **Operations** tab is used to manage the API's operations and is used in the following step in the tutorial, and the **Issues** tab can be used to view issues reported by the developers using your APIs.

>The sample echo API doesn't use authentication, but for more information about configuring authentication, see [Configure API settings][].

Once an API is created and the settings configured, the next step is to add the operations to the API.

## <a name="add-operation"> </a>Add an operation

Click **Operations** to display the operations pane for the API. Since we have not yet added any operations, there are none displayed. 

![api-management-myecho-operations][]

Click **add operation** to add a new operation. The **New operation** window will be displayed and the **Signature** tab will be selected by default.

![api-management-operation-signature][]

In this example, we will specify a GET operation on the echo service. Enter the following values into the fields on the **Signature** tab.

-	Type **GET** into the **HTTP verb** text box. As you start typing you can select **GET** from the displayed list of http verbs.
-	Type **/resource** into the **URL template** text box.
-	Type **GET resource** into the **Display** name text box.
-	Type **A demonstration of a GET call on a sample resource. It is handled by an "echo" backend which returns a response equal to the request (the supplied headers and body are being returned as received).** into the **Description** text box. This description is used to generate documentation for this operation when developers use this API.

Click **Parameters** to configure the query string parameters for this operation. In this example there are two query string parameters. To add a query parameter click **Add query parameter** and specify the following values.

For the first query parameter, configure the following values.

-	Type **param1** into the **Name** text box.
-	Type **A sample parameter that is required.** into the **Description** text box.
-	Click the **Type** field and choose **string** from the list. Supported types are **string**, **number**, **boolean**, and **dateTime**.
-	Click the **Values** field, type **sample** into the text box, and click the plus sign to add the default value text to the parameter. After adding the default text, click anywhere outside the **Values** field to dismiss the add value window.
-	Check the **Required** check box.

For the second query parameter, enter the following values.

-	**Name**: **param2**
-	**Description**: **Another sample parameter, set to not required.**
-	**Type**: **number**

It is a good practice to provide examples of responses for all status codes that the operation may produce. Each status code may have more than one response body example, one for each of the supported content types. In this tutorial we are adding a **200 OK** response code.

Click **Add** in the Responses section, start typing **200** into the text box, and then select **200 OK** from the drop-down list. 

![api-management-add-response][]

Once **200 OK** is selected, a new response code is added to the operation and the response window is displayed. Type **Returned in all cases.** into the **Description** text box.

![api-management-add-response-window][]

>**Add Representation** is used to configure responses in multiple representations. For more information, see [Responses][].

Click **Save** to add the newly configured operation to the API.

>It is not required to click **Save** after configuring each tab when adding a new operation, but be sure to save when you are complete. If you want to save after configuring each tab, click **Edit** for the operation to return to the configuration tab.

## <a name="add-api-to-product"> </a>Add the new API to a product

In API Management, developers subscribe to a product in order to use the product's APIs. Each product contains one or more APIs, as well as a usage quota and the terms of use. Before an API can be used by developers it must be added to a product and published. In this step of the tutorial you will add the **My Echo API** to a product.

Click **Products** from the **API Management** menu on the left to view and configure the products available in this API Instance.

![api-management-list-products][]

By default, each API Management instance comes with two sample products:

-	**15 Day Free Trial**
-	**Unlimited**

In this tutorial we will use the **15 Day Free Trial** product. Click **Configure** for the **15 Day Free Trial** to view the settings, including the APIs that are associated with that product.

![api-management-add-api-to-product][]

Click **Add API to product**.

![api-management-add-myechoapi-to-product][]

Check the box for **My Echo API**, and click **Save**.

![api-management-api-added-to-product][]

Now that **My Echo API** is associated with a product, developers can subscribe to and begin using the API.

>This tutorial step used the 15 Day Free Trial product, which comes pre-configured and ready for use. For a step-by-step guide on creating and publishing a new product, see [How create and publish a product][].

## <a name="subscribe"> </a>Subscribe to the product that contains the API

In order to use the APIs in a product, developers must be subscribed to the product. Developers can subscribe to products in the Developer portal, and administrators can subscribe developers to products in the Management portal. You are an administrator by default since you created the API Management instance in the previous steps in the tutorial, so you will subscribe your account to the 15 Day Free Trial product.

Click **Developers** from the **API Management** menu on the left to view and configure the developers in this service instance.

![api-management-developers][]

Click **Details** to the right of the **Admin** user to configure the settings for the user, including subscriptions.

![api-management-add-subscription][]

Click **Add Subscription**.

![api-management-add-subscription-window][]

Check the box for **15 Day Free Trial** and click **Subscribe**.

![api-management-subscription-added][]

Once your developer account is subscribed, you can call that product's APIs.

## <a name="call-operation"> </a>Call an operation from the Developer Portal

Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API. In this tutorial step you will call the Get method that was added to **My Echo API**. Click **Developer portal** from the menu at the top right of the Management portal.

![api-management-developer-portal-menu][]

Click **APIs** from the top menu, and then click **My Echo API** to see the operations available.

![api-management-developer-portal-myecho-api][]

Note that the description and parameters that were added when you created the operation are displayed, providing documentation for the developers that will use this operation.

Click **Open Console**. 

![api-management-developer-portal-myecho-api-console][]

Enter some values for the parameters, and enter your developer key. Keys are found in the **Your account** page of the Management portal. To view your key directly from the  current page in the Developer portal, right-click **Your account** and select **Open in new tab**. Switch to the new tab and copy either the primary or secondary key.

>To view **Your account** from within the Administrative portal, select **View Account** from the menu at the top right of the portal.

![api-management-developer-key][]

Switch back to the Developer portal, enter your key, and click **HTTP Get**.

![api-management-invoke-get][]

After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**. 

![api-management-invoke-get-response][]


## <a name="view-analytics"> </a>View analytics

To view analytics for **My Echo API**, switch back to the Administrative portal by selecting **Manage** from the user menu at the top right of the Developer portal.

![api-management-manage-menu][]

The default view for the Administrative portal is the Dashboard, which provides an overview of your API Management instance.

![api-management-dashboard][]

Hover the mouse over the chart for My Echo API to see the specific metrics for the usage of the API for a given time period.

>If you don't see any lines on your chart, switch back to the Developer portal and make some calls into the API, wait a few moments, and then come back to the Dashboard.

![api-management-mouse-over][]

Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.

![api-management-api-summary-metrics][]

For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.

![api-management-analytics-overview][]

The **Analytics** section has the following four tabs.

-	**At a glance** provides overall usage and health metrics as well as the top developers, top products, top APIs, and top operations.
-	**Usage** allows you to query for specific date ranges, products, APIs, and operations, and shows a geographical representation of calls and bandwidth usage.
-	**Health** focuses on status codes, cache, response times, and API and service response times, which allow you to monitor the health of your API Management instance.
-	**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.

For more information on viewing analytics, see [Analytics and monitoring][]. (Link TODO)

## <a name="next-steps"> </a>Next steps

TODO: link to the advance tutorial landing page with sublinks to each individual item.

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps

[Configure API settings]: ./api-management-hotwo-create-apis/#configure-api-settings
[Responses]: ./api-management-howto-add-operations/#responses
[How create and publish a product]: ./api-management-howto-add-products

[Management Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./Media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./Media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./Media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./Media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./Media/api-management-get-started/api-management-instance-created.png
[api-management-create-api]: ./Media/api-management-get-started/api-management-create-api.png
[api-management-add-new-api]: ./Media/api-management-get-started/api-management-add-new-api.png
[api-management-new-api-summary]: ./Media/api-management-get-started/api-management-new-api-summary.png
[api-management-myecho-operations]: ./Media/api-management-get-started/api-management-myecho-operations.png
[api-management-operation-signature]: ./Media/api-management-get-started/api-management-operation-signature.png
[api-management-list-products]: ./Media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./Media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./Media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./Media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./Media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./Media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./Media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./Media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./Media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-myecho-api]: ./Media/api-management-get-started/api-management-developer-portal-myecho-api.png
[api-management-developer-portal-myecho-api-console]: ./Media/api-management-get-started/api-management-developer-portal-myecho-api-console.png
[api-management-invoke-get]: ./Media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./Media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./Media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./Media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./Media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./Media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./Media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./Media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./Media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./Media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./Media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./Media/api-management-get-started/api-management-.png
[api-management-]: ./Media/api-management-get-started/api-management-.png