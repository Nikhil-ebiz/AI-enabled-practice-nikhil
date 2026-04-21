# Feature Request

**Product:** Gmail
**Feature request:**  
"Can we make it easier to temporarily mute certain email threads during specific times of the day without fully snoozing or muting them?"

# Engineering Brief

**What are we building?**

- We are building a Gmail feature that allows users to temporarily mute certain email threads during specific times of the day without fully snoozing or muting them.

## Problem Statement

**Why are we building it?**

- Currently, users cannot mute email threads during specific times of the day without fully snoozing or muting them.
- Assuming users have a time slot dedicated for dedicated focused work, they would like to be able to mute their email threads during that time slot without having to fully snooze or mute them.
- Currently, users have to manually mute and unmute notifications for each email thread individually and on daily basis.

## Assumptions

- We assume that users would like to be able to mute selected email threads for a weekly scheduled time. (Daily scheduled time can be set by a "Set for all days" option and monthly scheduled is not required for this feature.)
- User should get the notification of the snoozed email threads after scheduled focus time is over.

## Acceptance Criteria

- User should not get the notification of the snoozed email threads in scheduled focus time.
- Unsnoozed email thread's notification should be unaffected.
- User can have single email account logged to multiple devices, and none of them should get notification if notifications are snoozed per that device's timezone.

## Risks

- Email sender, recipient and email server can be in different timezones.
- User can login to multiple devices, and those devices can be in different timezones.
- UI will have to be designed to show multiple time windows and threads snoozed by the user clearly.
