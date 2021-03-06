# TypeScript typings for Google Play EMM API v1
Manages the deployment of apps to Android for Work users.
For detailed description please check [documentation](https://developers.google.com/android/work/play/emm-api).

## Installing

Install typings for Google Play EMM API:
```
npm install @types/gapi.client.androidenterprise@v1 --save-dev
```

## Usage

You need to initialize Google API client in your code:
```typescript
gapi.load("client", () => { 
    // now we can use gapi.client
    // ... 
});
```

Then load api client wrapper:
```typescript
gapi.client.load('androidenterprise', 'v1', () => {
    // now we can use gapi.client.androidenterprise
    // ... 
});
```

Don't forget to authenticate your client before sending any request to resources:
```typescript

// declare client_id registered in Google Developers Console
var client_id = '',
    scope = [     
        // Manage corporate Android devices
        'https://www.googleapis.com/auth/androidenterprise',
    ],
    immediate = true;
// ...

gapi.auth.authorize({ client_id: client_id, scope: scope, immediate: immediate }, authResult => {
    if (authResult && !authResult.error) {
        /* handle succesfull authorization */
    } else {
        /* handle authorization error */
    }
});            
```

After that you can use Google Play EMM API resources:

```typescript 
    
/* 
Retrieves the details of a device.  
*/
await gapi.client.devices.get({ deviceId: "deviceId", enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Retrieves whether a device's access to Google services is enabled or disabled. The device state takes effect only if enforcing EMM policies on Android devices is enabled in the Google Admin Console. Otherwise, the device state is ignored and all devices are allowed access to Google services. This is only supported for Google-managed users.  
*/
await gapi.client.devices.getState({ deviceId: "deviceId", enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Retrieves the IDs of all of a user's devices.  
*/
await gapi.client.devices.list({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Sets whether a device's access to Google services is enabled or disabled. The device state takes effect only if enforcing EMM policies on Android devices is enabled in the Google Admin Console. Otherwise, the device state is ignored and all devices are allowed access to Google services. This is only supported for Google-managed users.  
*/
await gapi.client.devices.setState({ deviceId: "deviceId", enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Acknowledges notifications that were received from Enterprises.PullNotificationSet to prevent subsequent calls from returning the same notifications.  
*/
await gapi.client.enterprises.acknowledgeNotificationSet({  }); 
    
/* 
Completes the signup flow, by specifying the Completion token and Enterprise token. This request must not be called multiple times for a given Enterprise Token.  
*/
await gapi.client.enterprises.completeSignup({  }); 
    
/* 
Returns a unique token to access an embeddable UI. To generate a web UI, pass the generated token into the managed Google Play javascript API. Each token may only be used to start one UI session. See the javascript API documentation for further information.  
*/
await gapi.client.enterprises.createWebToken({ enterpriseId: "enterpriseId",  }); 
    
/* 
Deletes the binding between the EMM and enterprise. This is now deprecated. Use this method only to unenroll customers that were previously enrolled with the insert call, then enroll them again with the enroll call.  
*/
await gapi.client.enterprises.delete({ enterpriseId: "enterpriseId",  }); 
    
/* 
Enrolls an enterprise with the calling EMM.  
*/
await gapi.client.enterprises.enroll({ token: "token",  }); 
    
/* 
Generates a sign-up URL.  
*/
await gapi.client.enterprises.generateSignupUrl({  }); 
    
/* 
Retrieves the name and domain of an enterprise.  
*/
await gapi.client.enterprises.get({ enterpriseId: "enterpriseId",  }); 
    
/* 
Returns the Android Device Policy config resource.  
*/
await gapi.client.enterprises.getAndroidDevicePolicyConfig({ enterpriseId: "enterpriseId",  }); 
    
/* 
Returns a service account and credentials. The service account can be bound to the enterprise by calling setAccount. The service account is unique to this enterprise and EMM, and will be deleted if the enterprise is unbound. The credentials contain private key data and are not stored server-side.

This method can only be called after calling Enterprises.Enroll or Enterprises.CompleteSignup, and before Enterprises.SetAccount; at other times it will return an error.

Subsequent calls after the first will generate a new, unique set of credentials, and invalidate the previously generated credentials.

Once the service account is bound to the enterprise, it can be managed using the serviceAccountKeys resource.  
*/
await gapi.client.enterprises.getServiceAccount({ enterpriseId: "enterpriseId",  }); 
    
/* 
Returns the store layout for the enterprise. If the store layout has not been set, returns "basic" as the store layout type and no homepage.  
*/
await gapi.client.enterprises.getStoreLayout({ enterpriseId: "enterpriseId",  }); 
    
/* 
Establishes the binding between the EMM and an enterprise. This is now deprecated; use enroll instead.  
*/
await gapi.client.enterprises.insert({ token: "token",  }); 
    
/* 
Looks up an enterprise by domain name. This is only supported for enterprises created via the Google-initiated creation flow. Lookup of the id is not needed for enterprises created via the EMM-initiated flow since the EMM learns the enterprise ID in the callback specified in the Enterprises.generateSignupUrl call.  
*/
await gapi.client.enterprises.list({ domain: "domain",  }); 
    
/* 
Pulls and returns a notification set for the enterprises associated with the service account authenticated for the request. The notification set may be empty if no notification are pending.
A notification set returned needs to be acknowledged within 20 seconds by calling Enterprises.AcknowledgeNotificationSet, unless the notification set is empty.
Notifications that are not acknowledged within the 20 seconds will eventually be included again in the response to another PullNotificationSet request, and those that are never acknowledged will ultimately be deleted according to the Google Cloud Platform Pub/Sub system policy.
Multiple requests might be performed concurrently to retrieve notifications, in which case the pending notifications (if any) will be split among each caller, if any are pending.
If no notifications are present, an empty notification list is returned. Subsequent requests may return more notifications once they become available.  
*/
await gapi.client.enterprises.pullNotificationSet({  }); 
    
/* 
Sends a test notification to validate the EMM integration with the Google Cloud Pub/Sub service for this enterprise.  
*/
await gapi.client.enterprises.sendTestPushNotification({ enterpriseId: "enterpriseId",  }); 
    
/* 
Sets the account that will be used to authenticate to the API as the enterprise.  
*/
await gapi.client.enterprises.setAccount({ enterpriseId: "enterpriseId",  }); 
    
/* 
Sets the Android Device Policy config resource. EMM may use this method to enable or disable Android Device Policy support for the specified enterprise. To learn more about managing devices and apps with Android Device Policy, see the Android Management API.  
*/
await gapi.client.enterprises.setAndroidDevicePolicyConfig({ enterpriseId: "enterpriseId",  }); 
    
/* 
Sets the store layout for the enterprise. By default, storeLayoutType is set to "basic" and the basic store layout is enabled. The basic layout only contains apps approved by the admin, and that have been added to the available product set for a user (using the  setAvailableProductSet call). Apps on the page are sorted in order of their product ID value. If you create a custom store layout (by setting storeLayoutType = "custom" and setting a homepage), the basic store layout is disabled.  
*/
await gapi.client.enterprises.setStoreLayout({ enterpriseId: "enterpriseId",  }); 
    
/* 
Unenrolls an enterprise from the calling EMM.  
*/
await gapi.client.enterprises.unenroll({ enterpriseId: "enterpriseId",  }); 
    
/* 
Removes an entitlement to an app for a user.  
*/
await gapi.client.entitlements.delete({ enterpriseId: "enterpriseId", entitlementId: "entitlementId", userId: "userId",  }); 
    
/* 
Retrieves details of an entitlement.  
*/
await gapi.client.entitlements.get({ enterpriseId: "enterpriseId", entitlementId: "entitlementId", userId: "userId",  }); 
    
/* 
Lists all entitlements for the specified user. Only the ID is set.  
*/
await gapi.client.entitlements.list({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Adds or updates an entitlement to an app for a user. This method supports patch semantics.  
*/
await gapi.client.entitlements.patch({ enterpriseId: "enterpriseId", entitlementId: "entitlementId", userId: "userId",  }); 
    
/* 
Adds or updates an entitlement to an app for a user.  
*/
await gapi.client.entitlements.update({ enterpriseId: "enterpriseId", entitlementId: "entitlementId", userId: "userId",  }); 
    
/* 
Retrieves details of an enterprise's group license for a product.  
*/
await gapi.client.grouplicenses.get({ enterpriseId: "enterpriseId", groupLicenseId: "groupLicenseId",  }); 
    
/* 
Retrieves IDs of all products for which the enterprise has a group license.  
*/
await gapi.client.grouplicenses.list({ enterpriseId: "enterpriseId",  }); 
    
/* 
Retrieves the IDs of the users who have been granted entitlements under the license.  
*/
await gapi.client.grouplicenseusers.list({ enterpriseId: "enterpriseId", groupLicenseId: "groupLicenseId",  }); 
    
/* 
Requests to remove an app from a device. A call to get or list will still show the app as installed on the device until it is actually removed.  
*/
await gapi.client.installs.delete({ deviceId: "deviceId", enterpriseId: "enterpriseId", installId: "installId", userId: "userId",  }); 
    
/* 
Retrieves details of an installation of an app on a device.  
*/
await gapi.client.installs.get({ deviceId: "deviceId", enterpriseId: "enterpriseId", installId: "installId", userId: "userId",  }); 
    
/* 
Retrieves the details of all apps installed on the specified device.  
*/
await gapi.client.installs.list({ deviceId: "deviceId", enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Requests to install the latest version of an app to a device. If the app is already installed, then it is updated to the latest version if necessary. This method supports patch semantics.  
*/
await gapi.client.installs.patch({ deviceId: "deviceId", enterpriseId: "enterpriseId", installId: "installId", userId: "userId",  }); 
    
/* 
Requests to install the latest version of an app to a device. If the app is already installed, then it is updated to the latest version if necessary.  
*/
await gapi.client.installs.update({ deviceId: "deviceId", enterpriseId: "enterpriseId", installId: "installId", userId: "userId",  }); 
    
/* 
Removes a per-device managed configuration for an app for the specified device.  
*/
await gapi.client.managedconfigurationsfordevice.delete({ deviceId: "deviceId", enterpriseId: "enterpriseId", managedConfigurationForDeviceId: "managedConfigurationForDeviceId", userId: "userId",  }); 
    
/* 
Retrieves details of a per-device managed configuration.  
*/
await gapi.client.managedconfigurationsfordevice.get({ deviceId: "deviceId", enterpriseId: "enterpriseId", managedConfigurationForDeviceId: "managedConfigurationForDeviceId", userId: "userId",  }); 
    
/* 
Lists all the per-device managed configurations for the specified device. Only the ID is set.  
*/
await gapi.client.managedconfigurationsfordevice.list({ deviceId: "deviceId", enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Adds or updates a per-device managed configuration for an app for the specified device. This method supports patch semantics.  
*/
await gapi.client.managedconfigurationsfordevice.patch({ deviceId: "deviceId", enterpriseId: "enterpriseId", managedConfigurationForDeviceId: "managedConfigurationForDeviceId", userId: "userId",  }); 
    
/* 
Adds or updates a per-device managed configuration for an app for the specified device.  
*/
await gapi.client.managedconfigurationsfordevice.update({ deviceId: "deviceId", enterpriseId: "enterpriseId", managedConfigurationForDeviceId: "managedConfigurationForDeviceId", userId: "userId",  }); 
    
/* 
Removes a per-user managed configuration for an app for the specified user.  
*/
await gapi.client.managedconfigurationsforuser.delete({ enterpriseId: "enterpriseId", managedConfigurationForUserId: "managedConfigurationForUserId", userId: "userId",  }); 
    
/* 
Retrieves details of a per-user managed configuration for an app for the specified user.  
*/
await gapi.client.managedconfigurationsforuser.get({ enterpriseId: "enterpriseId", managedConfigurationForUserId: "managedConfigurationForUserId", userId: "userId",  }); 
    
/* 
Lists all the per-user managed configurations for the specified user. Only the ID is set.  
*/
await gapi.client.managedconfigurationsforuser.list({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Adds or updates a per-user managed configuration for an app for the specified user. This method supports patch semantics.  
*/
await gapi.client.managedconfigurationsforuser.patch({ enterpriseId: "enterpriseId", managedConfigurationForUserId: "managedConfigurationForUserId", userId: "userId",  }); 
    
/* 
Adds or updates a per-user managed configuration for an app for the specified user.  
*/
await gapi.client.managedconfigurationsforuser.update({ enterpriseId: "enterpriseId", managedConfigurationForUserId: "managedConfigurationForUserId", userId: "userId",  }); 
    
/* 
Retrieves details of an Android app permission for display to an enterprise admin.  
*/
await gapi.client.permissions.get({ permissionId: "permissionId",  }); 
    
/* 
Approves the specified product and the relevant app permissions, if any. The maximum number of products that you can approve per enterprise customer is 1,000.

To learn how to use managed Google Play to design and create a store layout to display approved products to your users, see Store Layout Design.  
*/
await gapi.client.products.approve({ enterpriseId: "enterpriseId", productId: "productId",  }); 
    
/* 
Generates a URL that can be rendered in an iframe to display the permissions (if any) of a product. An enterprise admin must view these permissions and accept them on behalf of their organization in order to approve that product.

Admins should accept the displayed permissions by interacting with a separate UI element in the EMM console, which in turn should trigger the use of this URL as the approvalUrlInfo.approvalUrl property in a Products.approve call to approve the product. This URL can only be used to display permissions for up to 1 day.  
*/
await gapi.client.products.generateApprovalUrl({ enterpriseId: "enterpriseId", productId: "productId",  }); 
    
/* 
Retrieves details of a product for display to an enterprise admin.  
*/
await gapi.client.products.get({ enterpriseId: "enterpriseId", productId: "productId",  }); 
    
/* 
Retrieves the schema that defines the configurable properties for this product. All products have a schema, but this schema may be empty if no managed configurations have been defined. This schema can be used to populate a UI that allows an admin to configure the product. To apply a managed configuration based on the schema obtained using this API, see Managed Configurations through Play.  
*/
await gapi.client.products.getAppRestrictionsSchema({ enterpriseId: "enterpriseId", productId: "productId",  }); 
    
/* 
Retrieves the Android app permissions required by this app.  
*/
await gapi.client.products.getPermissions({ enterpriseId: "enterpriseId", productId: "productId",  }); 
    
/* 
Finds approved products that match a query, or all approved products if there is no query.  
*/
await gapi.client.products.list({ enterpriseId: "enterpriseId",  }); 
    
/* 
Unapproves the specified product (and the relevant app permissions, if any)  
*/
await gapi.client.products.unapprove({ enterpriseId: "enterpriseId", productId: "productId",  }); 
    
/* 
Removes and invalidates the specified credentials for the service account associated with this enterprise. The calling service account must have been retrieved by calling Enterprises.GetServiceAccount and must have been set as the enterprise service account by calling Enterprises.SetAccount.  
*/
await gapi.client.serviceaccountkeys.delete({ enterpriseId: "enterpriseId", keyId: "keyId",  }); 
    
/* 
Generates new credentials for the service account associated with this enterprise. The calling service account must have been retrieved by calling Enterprises.GetServiceAccount and must have been set as the enterprise service account by calling Enterprises.SetAccount.

Only the type of the key should be populated in the resource to be inserted.  
*/
await gapi.client.serviceaccountkeys.insert({ enterpriseId: "enterpriseId",  }); 
    
/* 
Lists all active credentials for the service account associated with this enterprise. Only the ID and key type are returned. The calling service account must have been retrieved by calling Enterprises.GetServiceAccount and must have been set as the enterprise service account by calling Enterprises.SetAccount.  
*/
await gapi.client.serviceaccountkeys.list({ enterpriseId: "enterpriseId",  }); 
    
/* 
Deletes a cluster.  
*/
await gapi.client.storelayoutclusters.delete({ clusterId: "clusterId", enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Retrieves details of a cluster.  
*/
await gapi.client.storelayoutclusters.get({ clusterId: "clusterId", enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Inserts a new cluster in a page.  
*/
await gapi.client.storelayoutclusters.insert({ enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Retrieves the details of all clusters on the specified page.  
*/
await gapi.client.storelayoutclusters.list({ enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Updates a cluster. This method supports patch semantics.  
*/
await gapi.client.storelayoutclusters.patch({ clusterId: "clusterId", enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Updates a cluster.  
*/
await gapi.client.storelayoutclusters.update({ clusterId: "clusterId", enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Deletes a store page.  
*/
await gapi.client.storelayoutpages.delete({ enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Retrieves details of a store page.  
*/
await gapi.client.storelayoutpages.get({ enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Inserts a new store page.  
*/
await gapi.client.storelayoutpages.insert({ enterpriseId: "enterpriseId",  }); 
    
/* 
Retrieves the details of all pages in the store.  
*/
await gapi.client.storelayoutpages.list({ enterpriseId: "enterpriseId",  }); 
    
/* 
Updates the content of a store page. This method supports patch semantics.  
*/
await gapi.client.storelayoutpages.patch({ enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Updates the content of a store page.  
*/
await gapi.client.storelayoutpages.update({ enterpriseId: "enterpriseId", pageId: "pageId",  }); 
    
/* 
Deleted an EMM-managed user.  
*/
await gapi.client.users.delete({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Generates an authentication token which the device policy client can use to provision the given EMM-managed user account on a device. The generated token is single-use and expires after a few minutes.

This call only works with EMM-managed accounts.  
*/
await gapi.client.users.generateAuthenticationToken({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Generates a token (activation code) to allow this user to configure their managed account in the Android Setup Wizard. Revokes any previously generated token.

This call only works with Google managed accounts.  
*/
await gapi.client.users.generateToken({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Retrieves a user's details.  
*/
await gapi.client.users.get({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Retrieves the set of products a user is entitled to access.  
*/
await gapi.client.users.getAvailableProductSet({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Creates a new EMM-managed user.

The Users resource passed in the body of the request should include an accountIdentifier and an accountType.
If a corresponding user already exists with the same account identifier, the user will be updated with the resource. In this case only the displayName field can be changed.  
*/
await gapi.client.users.insert({ enterpriseId: "enterpriseId",  }); 
    
/* 
Looks up a user by primary email address. This is only supported for Google-managed users. Lookup of the id is not needed for EMM-managed users because the id is already returned in the result of the Users.insert call.  
*/
await gapi.client.users.list({ email: "email", enterpriseId: "enterpriseId",  }); 
    
/* 
Updates the details of an EMM-managed user.

Can be used with EMM-managed users only (not Google managed users). Pass the new details in the Users resource in the request body. Only the displayName field can be changed. Other fields must either be unset or have the currently active value. This method supports patch semantics.  
*/
await gapi.client.users.patch({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Revokes a previously generated token (activation code) for the user.  
*/
await gapi.client.users.revokeToken({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Modifies the set of products that a user is entitled to access (referred to as whitelisted products). Only products that are approved or products that were previously approved (products with revoked approval) can be whitelisted.  
*/
await gapi.client.users.setAvailableProductSet({ enterpriseId: "enterpriseId", userId: "userId",  }); 
    
/* 
Updates the details of an EMM-managed user.

Can be used with EMM-managed users only (not Google managed users). Pass the new details in the Users resource in the request body. Only the displayName field can be changed. Other fields must either be unset or have the currently active value.  
*/
await gapi.client.users.update({ enterpriseId: "enterpriseId", userId: "userId",  });
```