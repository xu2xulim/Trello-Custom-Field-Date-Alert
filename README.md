# Trello-Custom-Field-Date-Alert

Trello offers a notification system based on card due date and notification system documented at https://help.trello.com/article/793-receiving-trello-notifications .

While you can create custom field dates, there is no notification built around these dates.

This solution addresses the above by :

- create a alert record when there is a date set on a custom field date.
  - when a new date the alert record will be update with the new date
- a cron job will process all alerts with a "tracking" status and date that matches a pre-determined criterion.
- create a notification by create a comment using "@card some meaningful text"**.
- set a expiry on the alert record so that it is automatically removed from the alert file.

## Endpoints

### /cfdate_alert

This serves as the webhook endpoint to process updates to custom fields ,and in particular, those of type = 'date'. It creates an alert record.

### /setup

This creates a webhook in Trello based on the idModel using the board_id. This means that the system can be used concurrent for different boards.

### /stop

This deletes the webhook in Trello by a board and also remove all existing already records for the board.

The endpoint documentation is available at https://zlaxc3.deta.dev/redoc .

## Pre-requisites

The pre-requisites includes :
- the admin Trello API Key and Token in the .env file.
- defined criterion to be used for the cron job.

## Technical Notes

The solution components include :

- A Deta Micro using FastAPI deployed on deta.dev or other platform like Wayscript X.
  - a cron to process and create the alerts.
- A Deta Base for the alert records.
- Trello webhook using the board id as the idModel.

## Roadmap
Here's a list of enhancements on the roadmap.
- An exclusion list for custom field dates.
- A different alert days for different boards.
