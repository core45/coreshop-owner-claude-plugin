# Coreshop owner recipes for Claude Code

Optional. Your shop works fully without this plugin. It adds step-by-step recipes (research, checklists,
drafts) on top of the tools your shop's MCP server already gives Claude Code.

## Before you install

Connect your shop first: open "Claude & API access" in your shop's panel, create a token, and follow the
Claude Code steps on that page. This plugin does not connect anything by itself.

## Install

In Claude Code:

    /plugin marketplace add core45/coreshop-owner-claude-plugin
    /plugin install coreshop-owner@coreshop-owner

## Recipes

- **seo-blog-series**: plan, research and draft a series of blog posts on one topic.
- **product-launch**: an announcement, buyer FAQs and a banner for one product.
- **webinar-funnel**: invitation, agenda post, follow-up, FAQs and a banner for one webinar.

Each recipe first checks that your shop supports it. Older shops get a plain message instead of errors.
Recipes create drafts. Claude publishes only when you ask and your token allows it.
