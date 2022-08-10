---
title: "Admin Example"
slug: "itccwhirlpool-coupon-generator"
excerpt: "itccwhirlpool.coupon-generator@1.0.0"
hidden: true
createdAt: "2022-07-28T13:33:08.415Z"
updatedAt: "2022-07-28T13:33:08.415Z"
---
An example admin app that adds a menu button to the admin sidebar and a navigation via parameter example.

### How to develop admins

1. Admins always declare routes in `/admin/app/<route>`

2. Declare the `admin` builder in your manifest

3. When installed, the user navigates to `/admin/<route>`, but your app runs in an iframe that points to `/admin/app/<route>`.

4. You can develop directly in the `/admin/app` route for convenience, but don't forget to test it inside the iframe. :)

### Quickstart

1. Clone this repo

2. `yarn --cwd react/` for code completion

3. `vtex link`

4. Navigate to `workspace--account.myvtex.com/admin/app/example`