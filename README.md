# Role-Based Contact Automation with n8n

An n8n workflow that receives portfolio contact-form submissions through a webhook, prepares the submitted data, routes requests by subject, logs contact details in Google Sheets, and sends notifications or email replies.

## Overview

This project demonstrates a practical no-code/low-code automation pattern for handling inbound website inquiries.

### Workflow

1. **Webhook** — receives a `POST` request from a contact form.
2. **prepare_data** — maps the name, email, phone, subject, message, and timestamp into consistent fields.
3. **Switch** — routes submissions by subject:
   - Booking
   - Career
   - Complaint
   - General
   - Partnership
4. **Telegram** — sends a booking notification.
5. **Google Sheets** — appends contact details to a spreadsheet.
6. **Gmail** — sends an internal notification and/or an acknowledgement email, depending on the route.

## Tech Stack

- n8n workflow automation
- Webhooks and JSON payloads
- Google Sheets
- Gmail
- Telegram Bot API

## Example Request

Configure your webhook to accept a JSON body like:

```json
{
  "user_name": "Jane Doe",
  "user_email": "jane@example.com",
  "phone": "+1-555-0100",
  "subject": "Booking",
  "message": "I would like to discuss a booking."
}
```

The workflow maps the incoming values from `body.user_name`, `body.user_email`, `body.phone`, `body.subject`, and `body.message`.

## Setup

1. Install or access an n8n instance.
2. Import `workflow.json` into n8n.
3. Configure the Webhook node and use your own test/production webhook URL.
4. Connect your own Telegram, Google Sheets, and Gmail credentials.
5. Select your own spreadsheet and worksheet, and map the expected columns:
   `Date`, `Name`, `Email`, `Phone`, `Subject`, `Message`.
6. Review every Switch rule and confirm the intended destinations for all five categories.
7. Test with sample submissions before activating the workflow.

## Security Notes

- The included workflow export is sanitized for sharing. Reconnect credentials and replace placeholder destinations before use.
- Do not commit API tokens, OAuth secrets, private webhook URLs, personal contact data, or production spreadsheet IDs.
- Use test accounts and sample data while developing.

## Known Limitations

This repository is based on a workflow export and has not been represented as production-tested. Review the Switch conditions and branch connections in n8n before use. In particular, verify that each category matches the intended subject and that notifications and acknowledgements are sent only to the intended recipients.

## Future Improvements

- Add robust validation and a clear fallback route for unknown subjects.
- Add error handling and retry logic for integrations.
- Add spam protection and rate limiting.
- Add execution logging and monitoring.
- Add a test matrix for each category.

## License

Choose a license before making this repository public. For example, add an MIT `LICENSE` file if you want to allow reuse under those terms.
