---
name: daily-email-digest
description: >
  Generate a daily prioritized email digest from the user's inbox (Gmail or Outlook).
  Use this skill whenever the user asks to summarize, check, review, or digest their emails,
  inbox, or messages — especially with phrases like "总结我的邮件", "check my emails",
  "what's in my inbox", "邮件摘要", "daily digest", or "catch me up on emails".
  Also trigger when the user asks what they need to reply to, or what's important in their inbox.
  Requires a Gmail or Outlook/Microsoft email MCP connector to be connected.
---

# Daily Email Digest

Generate a prioritized summary of the user's inbox (Gmail or Outlook) for the past 48 hours.

## Step 1: Check Connector

Before fetching emails, confirm a Gmail or Outlook/Microsoft email MCP tool is available and connected.
If not, tell the user they need to connect either Gmail or Outlook (Microsoft 365) and suggest they check
the tools/connectors menu.

## Step 2: Ask for Language Preference (if not already specified)

If the user hasn't specified a language for the digest output, ask:

> "你希望摘要用什么语言输出？（跟随邮件语言 / 中文 / 英文）"

- **跟随邮件语言**：Each email's summary is written in the same language as the email itself.
- **中文**：All summaries in Chinese regardless of email language.
- **英文**：All summaries in English regardless of email language.

## Step 3: Fetch Emails

Retrieve all emails from the past 48 hours using whichever connector is available — Gmail or Outlook. Both are supported; use whichever MCP tool is active in the current conversation.
Filter to: **unread emails** + **emails flagged as High Importance**.

## Step 4: Classify & Prioritize

Assign each email a priority tier using this order:

| Priority | Criteria |
|----------|----------|
| 🔴 High | Marked as **High Importance** by sender |
| 🟠 Medium-High | From a **teacher, professor, supervisor, or employer** |
| 🟡 Medium | From a **school, university, or institutional address** (e.g. admissions, registrar, student services) — events, notices, optional reads |
| ⚪ Low | **Unknown senders**, newsletters, automated notifications, **promotional/advertising emails** |

Within each tier, sort by **most recent first**.

Emails that are already read AND not High Importance can be skipped unless the user asks to include them.

## Step 5: Output Format

Present the digest as a clean, scannable summary. Use this structure:

---

### 📬 邮件摘要 · 过去 48 小时
**共 X 封未读 / Y 封重要邮件**

### ✅ 今日待办（从邮件中提取）
- [ ] 需要回复 [某人] 关于 [某事] — 截止：[日期或"尽快"]
- [ ] 确认 [某事项]

---

#### 🔴 高优先级
**[发件人名] — [主题]** · *时间*
> 摘要：1-2 句话说明邮件内容，以及是否需要回复或采取行动。
> ⚡ 建议操作：[回复 / 确认 / 无需操作]

---

#### 🟠 老师 / 导师 / 雇主
（同上格式）

---

#### 🟡 学校 / 机构通知
**[发件人名] — [主题]** · *时间*
> 一句话说明邮件内容（活动、通知等，无需操作提示）

*（每封单独一行，简洁即可，不加入待办清单）*

---

#### ⚪ 其他（低优先级）
> 共 X 封：包括来自 [来源A]、[来源B] 的通知/广告邮件，均无需操作。

---

## Notes

- Keep summaries concise: 1–2 sentences per email max.
- If an email is part of a thread, summarize the **latest reply** only, and note it's a thread.
- 🟡 School/institutional emails: summarize each one briefly (1 sentence), but **do NOT add them to the todo list** — they are informational only.
- ⚪ Low priority (unknown senders, newsletters, ads, promotions): **always group into a single line**, e.g. "3 封广告/通知邮件（来自 X、Y、Z）— 无需操作". Never list them individually.
- This skill is designed for **work/study inboxes** — assume the user's emails are professional or academic in nature.
- Always end with the **✅ 今日待办** section, even if it's empty ("无需操作的邮件").
- If there are 0 unread emails, say so cheerfully and confirm the inbox is clear.
