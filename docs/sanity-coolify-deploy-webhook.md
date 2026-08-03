# Rebuild Astro from Sanity

The Astro site is statically generated. A published Sanity document is therefore
only visible after Coolify has built and deployed the site again.

Sanity can trigger that deployment directly through Coolify's authenticated
deploy webhook. No webhook endpoint is needed in the Astro application.

## 1. Create a restricted Coolify token

In Coolify:

1. Open **Keys & Tokens** and select **API Tokens**.
2. Create a token named `Sanity deploy oddblog`.
3. Give the token only the **Deploy** permission.
4. Copy the token. It is only shown once.

Do not add the token to this repository or to an Astro environment variable.

## 2. Copy the application's deploy webhook

1. Open the `oddblog` application in Coolify.
2. Open **Webhooks**.
3. Copy the **Deploy Webhook** URL.

The URL normally points to Coolify's `/api/v1/deploy` endpoint and contains the
application UUID. Treat the URL as sensitive even though it also requires the
token.

## 3. Create the Sanity webhook

Open [Sanity Manage](https://www.sanity.io/manage), select this project, and go
to **API > Webhooks**. Create a webhook with these values:

| Field | Value |
| --- | --- |
| Name | `Rebuild oddblog in Coolify` |
| Description | `Rebuild the static Astro frontend when a post is published, changed, unpublished, or deleted.` |
| URL | The **Deploy Webhook** URL copied from Coolify |
| Dataset | The production dataset used by `PUBLIC_SANITY_DATASET` in Coolify |
| Trigger on | **Create**, **Update**, and **Delete** |
| Filter | `_type == "post"` |
| Projection | Leave empty |
| HTTP method | **GET** |
| API version | `2025-02-19` or newer |
| Include drafts | **Off** |
| Include versions | **Off** |
| Status | **Enabled** |

Add this HTTP header:

| Header | Value |
| --- | --- |
| `Authorization` | `Bearer COOLIFY_API_TOKEN` |

Replace `COOLIFY_API_TOKEN` with the restricted token from step 1. Do not add a
Sanity webhook **Secret**: that feature signs requests for a receiving endpoint,
whereas Coolify authenticates this request with the bearer token above.

Drafts must remain disabled. Publishing creates or updates the non-draft `post`
document and triggers a deployment; editing an unpublished draft does not.
Listening for delete also rebuilds the site when a post is unpublished or
deleted, so stale static pages disappear on the next deployment.

## 4. Test the complete flow

1. Publish a new post with a unique slug in Sanity Studio.
2. In Sanity Manage, open the webhook's **Attempts** log. The Coolify response
   should have a `2xx` status.
3. In Coolify, open the application's **Deployments** view and confirm that a new
   deployment was queued.
4. After it succeeds, open
   [the preview site](https://oddblog.preview.na-kreativ.dev/) and verify both the
   post list and `/blog/<slug>/`.

If Sanity reports `401`, recreate or correct the bearer token. If it reports
`404`, copy the current deploy webhook URL from the correct Coolify application.
If Coolify deploys successfully but the post is absent, verify that Coolify has
the same `PUBLIC_SANITY_PROJECT_ID` and `PUBLIC_SANITY_DATASET` values as the
Studio.
