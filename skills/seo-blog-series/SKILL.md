---
name: seo-blog-series
description: Plan, research and draft an SEO blog series for a Coreshop shop through its MCP server. Use when the owner asks for several blog posts on one topic, a content calendar or SEO articles for the shop.
---

# SEO blog series

Tools used: `get_shop_context`, `list_posts`, `get_post`, `create_posts`, `update_post`, `upload_image`, `publish_post`

Requires shop context schema_version 2 or later, with the capability posts.

## 1. Check the shop

- Call `get_shop_context` on the shop's MCP server.
- If `schema_version` is below 2, or `capabilities` does not list `posts`, stop and tell the owner:
  "Your shop does not support blog recipes yet. Ask your developer to update it."
- Note the locales, the default locale, the brand voice, the audience, the product categories and the
  `content_rules`. Note `access.content_level`: with `read`, only research is possible; tell the owner.

## 2. Research before writing

- Ask the owner for the topic, the number of posts (at most the batch size of `create_posts`) and the
  audience, if they did not say.
- Call `list_posts` with the topic's main terms. Open close matches with `get_post`. Never repeat a post the
  shop already has; propose an angle that links to it instead.
- If web search is available, check what ranks for the main terms and which questions people ask. Use it
  for angles only; never copy text, and never take product facts from the web.

## 3. Plan

- Propose one line per post: title, search intent (learn, compare, buy), main keyword and angle.
- Wait for the owner to agree or change the plan.

## 4. Write

Checklist per post:

- [ ] title under 60 characters, with the main keyword
- [ ] excerpt of one or two sentences
- [ ] body with headings, short paragraphs and one clear next step for the reader
- [ ] SEO fields written by you: seo_title (under 60 characters), seo_description (under 160) and seo_keywords
- [ ] only facts the shop provides; no claim that `content_rules` forbids
- [ ] written in the default locale

## 5. Create drafts

- Create all posts in one `create_posts` call. Say `format` `markdown` if you wrote Markdown.
- Show the owner every panel edit link the result returns.

## 6. Other languages and images

- Write the translations for the other active locales (listed by `get_shop_context`) yourself: natural, not
  word-for-word, same facts, localized slug. Each locale needs title, slug, excerpt, main_text and the SEO
  fields.
- Save them with `update_post` per post (post_id, expected_version from the create result, `translations`
  per locale; a new language needs a title), or include them in `create_posts`.
- Images: ask the owner for images and upload them with `upload_image`, then put the returned embed_html in
  the body; or leave the post without images.
- Never use the shop's own AI tools for text, translation, SEO or images unless the owner explicitly asks;
  they cost the shop money. If the owner asks for a shop-generated image, say it is a paid feature and the
  owner must first set a monthly AI cap on the "Claude & API access" page.

## 7. Publish only when asked

- With `access.content_level` `publish` and the owner's go-ahead, publish with `publish_post`; pass
  `publish_at` to schedule. Otherwise the owner publishes in the panel.
