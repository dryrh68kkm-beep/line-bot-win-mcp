# Main Menu Rich Menu Config

`main-menu.json` defines the 6-button LINE OA main menu:

```
LINE OA
├── 💬 ถาม Policy บริษัท        (message action, handled in-chat)
├── 🚨 แจ้งเหตุ 24H              (uri -> 24h-incident-report)
├── 📦 เช็กสินค้าใกล้หมดอายุ      (uri -> expiry-dashboard)
├── 🔎 ค้นหาสินค้า / Barcode     (uri -> scan-form)
├── 📊 ดูข้อมูลสรุป              (uri -> Dashboard)
└── 🤖 ผู้ช่วย AI                (message action, handled in-chat)
```

Six actions map onto `richmenu-template/template-06.md` (a 3x2 grid), so
this file can be passed directly as the `actions` input to the
`create_rich_menu` MCP tool.

## Before creating the rich menu

Replace the placeholder `uri` values with the real URLs (or LIFF URLs) of
each sub-system once they're available:

- `REPLACE_WITH_24H_INCIDENT_REPORT_URL` -> 24h-incident-report
- `REPLACE_WITH_EXPIRY_DASHBOARD_URL` -> expiry-dashboard
- `REPLACE_WITH_SCAN_FORM_URL` -> scan-form
- `REPLACE_WITH_DASHBOARD_URL` -> Dashboard

## Creating the rich menu

Ask the AI Agent connected to this MCP server to call `create_rich_menu`
with `chatBarText` and `actions` taken from `main-menu.json`. The tool
generates the menu image from `richmenu-template/template-06.md`,
uploads it, and sets it as the default rich menu.

The two message actions (`ถาม Policy บริษัท`, `ผู้ช่วย AI`) send that text
back into the chat as if the user typed it — wire up your bot's message
handler (outside this MCP server, e.g. a LINE webhook receiver) to react
to those two strings and route to the policy Q&A / AI assistant flow.
