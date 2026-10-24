# Broom

Broom keeps Gmail inboxes clear of promos and spam. On a schedule it reads each inbox, lists coupon codes it finds, and moves junk threads to Trash.

Broom is a skills-only Cursor plugin. It does not ship an MCP server. It uses the Gmail connector the user already has (the Gmail plugin). Submit this public repository where the marketplace form asks for an MCP server URL or a public GitHub repository.

## What it does

Two skills:

- `broom-getting-started` asks, one question at a time, which inboxes to clean, what to call the assistant, the schedule, senders to protect or always trash, and how to handle coupons. It saves those answers to the assistant's memory and creates a recurring routine that runs `junk-mail-check`.
- `junk-mail-check` is the cleanup run. It trashes marketing and spam, leaves protected mail in the inbox, and reports what it did.

The default schedule is hourly from about 7:30 AM to 9:30 PM in the user's time zone. Outside those hours a run stays quiet.

## Safety

- Trash only. Broom moves a thread to Gmail Trash. It does not permanently delete mail, empty Trash, or delete from Trash.
- It does not unsubscribe, and it does not click unsubscribe links, unless the user explicitly asks.
- It protects bank, card, brokerage, and payment mail; security alerts, sign-in mail, and one-time codes; orders and delivery confirmations; personal mail; and the other protected categories in `junk-mail-check`.
- On a business inbox it trashes only obvious marketing and spam.
- Anything borderline stays in the inbox and is listed for the user.
- A run that trashes nothing, holds nothing, and has nothing important to flag sends no report.

## Requirements

- A connected Gmail connector (install the Gmail plugin and sign in to each inbox Broom should clean).
- Broom itself adds no server, no extra account, and no API key.

## Install and get started

1. Install the Gmail plugin. Sign in to every inbox Broom should clean.
2. Install Broom from the Cursor marketplace after it is listed, or submit `https://github.com/onlymehdi/broom` at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).
3. To try the plugin before it is listed, clone this repo into `~/.cursor/plugins/local/broom` and reload Cursor. Open Customize and confirm the `broom-getting-started` and `junk-mail-check` skills are present.
4. In chat, run `/broom-getting-started` and answer one question at a time.
5. After the read-back, Broom saves the settings, creates the routine, and offers a first cleanup.

## Testing

1. Install Broom and install the Gmail plugin.
2. Connect Gmail for an inbox that contains both promo mail and mail that must stay (bank, security, or an order).
3. Run `broom-getting-started`. Name that inbox, pick a schedule, and leave protected-sender lists empty if you have none.
4. Run a cleanup with `junk-mail-check`, or accept the first cleanup when setup offers it.
5. In Gmail, confirm promo threads are in Trash and can be restored. Confirm bank, security, and order mail is still in the inbox.
6. Confirm the report lists each trashed email (sender, subject, and a few-word note) and every coupon code it found, with the minimum and expiry when the message has them. Confirm a later run that finds nothing sends no report.
7. Move a trashed thread back to the inbox, or trash something Broom left behind, and confirm Broom proposes a sender-rule change and waits for a yes before saving it.

## Logo

The marketplace logo is `assets/logo.png` (square PNG, background plate kept). On `main` the file is:

https://raw.githubusercontent.com/onlymehdi/broom/main/assets/logo.png

The manifest points at the relative path `assets/logo.png`. Cursor resolves that path to a `raw.githubusercontent.com` URL for the repository.

## License

MIT, copyright onlymehdi 2026. See [LICENSE](LICENSE).
