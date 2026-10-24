> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Manage API keys

> Learn how to view, edit, and delete your API keys in Resend.

## API keys

API keys are secret tokens used to authenticate your requests. They are unique to your account and must be kept confidential.

You can use multiple keys to isolate different application actions to different API keys. This allows you to [view logs per key](#view-api-key-logs), detect possible abuse, and control any damage that may be done accidentally or maliciously.

## API key management

You can view and manage your API keys from the [**API keys** Dashboard page](https://resend.com/api-keys). You can also manage your API keys programmatically using the [API](https://resend.com/docs/api-reference/api-keys/create-api-key.md) or the [Resend CLI](https://resend.com/docs/cli.md#api-keys):

* [Create](https://resend.com/docs/api-reference/api-keys/create-api-key.md) a new API key with a name, permission, and optional domain restriction
* [List](https://resend.com/docs/api-reference/api-keys/list-api-keys.md) all API keys in your account
* [Update](https://resend.com/docs/api-reference/api-keys/update-api-key.md) an API key's name (other properties can only be edited in the Dashboard)
* [Delete](https://resend.com/docs/api-reference/api-keys/delete-api-key.md) an API key

## View all API keys

The [API Dashboard](https://resend.com/api-keys) shows you all the API keys you have created along with their details, including the **last time you used** an API key.

Different color indicators let you quickly scan and detect which API keys are being used and which are not.

![View All API keys](https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-view-all.jpg?fit=max\&auto=format\&n=ABWmVTZIHGIFNTFD\&q=85\&s=f195ef7f60a110407e2739f30c10ca2a)

## Edit API key details

After [creating an API key](https://resend.com/docs/create-an-api-key.md), you can edit the following details:

* [Name](https://resend.com/docs/api-reference/api-keys/create-api-key.md#param-name)
* [Permission](https://resend.com/docs/api-reference/api-keys/create-api-key.md#param-permission)
* [Domain](https://resend.com/docs/api-reference/api-keys/create-api-key.md#domain-id)

> [!NOTE]
>
> You cannot view or edit an API key value after it has been created.

To edit an API key in the Resend Dashboard, click the **More options**  button and then **Edit API key**.

You can also rename an API key programmatically using the [Update API key endpoint](https://resend.com/docs/api-reference/api-keys/update-api-key.md). The API only updates the key's name, while permission and domain can only be edited in the Dashboard.

![View Inactive API key](https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-edit.jpeg?fit=max\&auto=format\&n=ABWmVTZIHGIFNTFD\&q=85\&s=7abe8e055cf311a7f66a40477db7946a)

## Delete inactive API keys

If an API key **hasn't been used in the last 30 days**, consider deleting it to keep your account secure.

![View Inactive API key](https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-view-inactive.jpg?fit=max\&auto=format\&n=ABWmVTZIHGIFNTFD\&q=85\&s=fa99650454696902100e03b669d3a9c1)

You can delete an API key by clicking the **More options**  button and then **Remove API key**.

![Delete API key](https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-remove.jpeg?fit=max\&auto=format\&n=ABWmVTZIHGIFNTFD\&q=85\&s=9fc76ff5dc4cd38f465539cd3a435706)

> [!TIP]
>
> See more [API key security practices](https://resend.com/docs/knowledge-base/how-to-handle-api-keys.md).

## View API key logs

When visualizing an active API key, you can see the **total number of requests** made to the key. For more detailed logging information, select the underlined number of requests to view all logs for that API key.

![View Active API key](https://mintcdn.com/resend/ABWmVTZIHGIFNTFD/images/dashboard-api-keys-view-active.jpg?fit=max\&auto=format\&n=ABWmVTZIHGIFNTFD\&q=85\&s=e0c0584545565e1e78e460b240d2c221)

## Export your data

Admins can download your data in CSV format for the following resources:

* Emails
* Broadcasts
* Contacts
* Segments
* Domains
* Logs
* API keys

> [!NOTE]
>
> Currently, exports are limited to admin users of your team.

To start, apply filters to your data and click on the "Export" button. Confirm your filters before exporting your data.

<video autoPlay muted loop playsinline src="https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/exports.mp4?fit=max&auto=format&n=OWNnQaVDyqcGyhhN&q=85&s=1149ee4e83b4414e75a0ecaa92774c38" />

If your exported data includes 1,000 items or less, the export will download immediately. For larger exports, you'll receive an email with a link to download your data.

All admins on your team can securely access the export for 7 days. Unavailable exports are marked as "Expired."

> [!NOTE]
>
> All exports your team creates are listed in the
> [Exports](https://resend.com/exports) page under **Settings** > **Team** >
> **Exports**. Select any export to view its details page. All members of your
> team can view your exports, but only admins can download the data.
