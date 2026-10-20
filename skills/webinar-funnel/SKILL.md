---
name: webinar-funnel
description: Plan the content around one webinar in a Coreshop shop through its MCP server - invitation, agenda post, follow-up, FAQs and a banner - using only the webinar records. Use when the owner promotes a webinar.
---

# Webinar funnel

Tools used: `get_shop_context`, `list_webinars`, `get_webinar`, `list_webinar_parts`, `create_posts`, `create_faqs`, `attach_faq`, `create_banner`, `set_banner_window`, `generate_post_images`, `translate_post`, `get_operation`, `publish_post`, `activate_banner`

Requires shop context schema_version 2 or later, with the capability webinars.

## 1. Check the shop

- Call `get_shop_context`. If `schema_version` is below 2, or `capabilities` does not list `webinars`, stop
  and tell the owner: "Your shop does not support webinar recipes yet. Ask your developer to update it."

## 2. Read the webinar

- If the owner gave no id, call `list_webinars` and let the owner pick.
- Call `get_webinar`, then `list_webinar_parts` for the agenda. Dates, speakers and content come only from
  these records; ask the owner for anything missing.

## 3. Plan the funnel

- Invitation post (why attend, when, who speaks), a what-you-will-learn post from the agenda, and a
  follow-up post for after the date. FAQs if `capabilities` lists `faqs`, a banner if it lists `banners`.
- Wait for the owner's go-ahead.

## 4. Create drafts

- [ ] the three posts in one `create_posts` call
- [ ] FAQs with `create_faqs`, then `attach_faq` to the invitation
- [ ] banner with `create_banner`, with a window ending when the webinar starts (`set_banner_window`)
- [ ] show the owner every panel edit link

## 5. Optional AI jobs (they cost the shop money)

- `generate_post_images` and `translate_post` only for the capabilities `get_shop_context` lists; follow each
  with `get_operation`.

## 6. Publish only when asked

- With `publish` access and the owner's go-ahead: `publish_post` (schedule the follow-up with `publish_at`)
  and `activate_banner`. Otherwise the owner publishes in the panel.
