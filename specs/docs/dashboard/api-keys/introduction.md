> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Manage API keys

> Learn how to view, edit, and delete your API keys in Resend.

## API keys

API keys are secret tokens used to authenticate your requests. They are unique to your account and must be kept confidential.

You can use multiple keys to isolate different application actions to different API keys. This allows you to [view logs per key](#view-api-key-logs), detect possible abuse, and control any damage that may be done accidentally or maliciously.

## API key management

You can view and manage your API keys from the [**API keys** Dashboard page](https://resend.com/api-keys). You can also manage your API keys programmatically using the [API](/docs/api-reference/api-keys/create-api-key) or the [Resend CLI](/docs/cli#api-keys):

* [Create](/docs/api-reference/api-keys/create-api-key) a new API key with a name, permission, and optional domain restriction
* [List](/docs/api-reference/api-keys/list-api-keys) all API keys in your account
* [Update](/docs/api-reference/api-keys/update-api-key) an API key's name (other properties can only be edited in the Dashboard)
* [Delete](/docs/api-reference/api-keys/delete-api-key) an API key

## View all API keys

The [API Dashboard](https://resend.com/api-keys) shows you all the API keys you have created along with their details, including the **last time you used** an API key.

Different color indicators let you quickly scan and detect which API keys are being used and which are not.

<img alt="View All API keys" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-view-all.jpg?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=f195ef7f60a110407e2739f30c10ca2a" width="2584" height="980" data-path="images/dashboard-api-keys-view-all.jpg" />

## Edit API key details

After [creating an API key](/docs/create-an-api-key), you can edit the following details:

* [Name](/docs/api-reference/api-keys/create-api-key#param-name)
* [Permission](/docs/api-reference/api-keys/create-api-key#param-permission)
* [Domain](/docs/api-reference/api-keys/create-api-key#domain-id)

<Info>You cannot view or edit an API key value after it has been created.</Info>

To edit an API key in the Resend Dashboard, click the **More options** <Icon icon="ellipsis" iconType="solid" /> button and then **Edit API key**.

You can also rename an API key programmatically using the [Update API key endpoint](/docs/api-reference/api-keys/update-api-key). The API only updates the key's name, while permission and domain can only be edited in the Dashboard.

<img alt="View Inactive API key" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-edit.jpeg?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=7abe8e055cf311a7f66a40477db7946a" width="1752" height="878" data-path="images/dashboard-api-keys-edit.jpeg" />

## Delete inactive API keys

If an API key **hasn't been used in the last 30 days**, consider deleting it to keep your account secure.

<img alt="View Inactive API key" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-view-inactive.jpg?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=fa99650454696902100e03b669d3a9c1" width="2584" height="980" data-path="images/dashboard-api-keys-view-inactive.jpg" />

You can delete an API key by clicking the **More options** <Icon icon="ellipsis" iconType="solid" /> button and then **Remove API key**.

<img alt="Delete API key" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-remove.jpeg?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=9fc76ff5dc4cd38f465539cd3a435706" width="2649" height="980" data-path="images/dashboard-api-keys-remove.jpeg" />

<Tip>
  See more [API key security practices](/docs/knowledge-base/how-to-handle-api-keys).
</Tip>

## View API key logs

When visualizing an active API key, you can see the **total number of requests** made to the key. For more detailed logging information, select the underlined number of requests to view all logs for that API key.

<img alt="View Active API key" src="https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-view-active.jpg?fit=max&auto=format&n=ABWmVTZIHGIFNTFD&q=85&s=e0c0584545565e1e78e460b240d2c221" width="2584" height="980" data-path="images/dashboard-api-keys-view-active.jpg" />

## Export your data

Admins can download your data in CSV format for the following resources:

* Emails
* Broadcasts
* Contacts
* Segments
* Domains
* Logs
* API keys

<Info>Currently, exports are limited to admin users of your team.</Info>

To start, apply filters to your data and click on the "Export" button. Confirm your filters before exporting your data.

<video autoPlay muted loop playsinline className="w-full aspect-video" src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/exports.mp4?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=1149ee4e83b4414e75a0ecaa92774c38" data-path="images/exports.mp4" />

If your exported data includes 1,000 items or less, the export will download immediately. For larger exports, you'll receive an email with a link to download your data.

All admins on your team can securely access the export for 7 days. Unavailable exports are marked as "Expired."

<Note>
  All exports your team creates are listed in the
  [Exports](https://resend.com/exports) page under **Settings** > **Team** >
  **Exports**. Select any export to view its details page. All members of your
  team can view your exports, but only admins can download the data.
</Note>
