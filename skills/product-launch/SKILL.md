---
name: product-launch
description: Prepare launch content for one product in a Coreshop shop through its MCP server - an announcement post, buyer FAQs and a banner - using only the product record. Use when the owner launches or promotes a product.
---

# Product launch

Tools used: `get_shop_context`, `list_products`, `get_product`, `create_posts`, `create_faqs`, `attach_faq`, `create_banner`, `set_banner_window`, `generate_post_images`, `translate_post`, `get_operation`, `publish_post`, `activate_banner`

Requires shop context schema_version 3 or later, with the capability products.

## 1. Check the shop

- Call `get_shop_context`. If `schema_version` is below 3, or `capabilities` does not list `products`, stop
  and tell the owner: "Your shop does not support product recipes yet. Ask your developer to update it."
- Note the locales, the brand voice, `content_rules` and `access`.

## 2. Find the product

- If the owner gave no id, call `list_products` with a search and let the owner pick.
- Call `get_product`. Everything you write comes from this record: names, descriptions, prices, variants,
  certificates. A certificate's backed claims are the only certification or food-contact claims allowed.
- List the facts you will use and ask the owner to fill any gap. Never invent a fact.

## 3. Plan the launch

- Propose: the announcement post; three to six buyer FAQs (if `capabilities` lists `faqs`); a banner (if it
  lists `banners`); the launch date. Wait for the owner's go-ahead.

## 4. Create drafts

- [ ] announcement with `create_posts`; link the product page only when `get_product` returns a public link
- [ ] FAQs with `create_faqs`, then `attach_faq` to the announcement
- [ ] banner with `create_banner`; with a launch date, a window with `set_banner_window`
- [ ] show the owner every panel edit link

## 5. Optional AI jobs (they cost the shop money)

- Offer `generate_post_images` and `translate_post` only for the capabilities `get_shop_context` lists;
  follow each with `get_operation`.

## 6. Go live only when asked

- With `access.content_level` `publish` and the owner's go-ahead: `publish_post` (pass `publish_at` for the
  launch day) and `activate_banner`. Otherwise the owner publishes in the panel.
