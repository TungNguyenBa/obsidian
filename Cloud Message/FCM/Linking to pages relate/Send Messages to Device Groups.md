- Device group messaging = Topic message but:
	- Manage group membership by **server** not by **client** to sub/unsub
	- Must be **authen** --> Only server has the right to add/delete devices in the group
- Use case:
	- Want to classify devices into separate groups according to backend logic (eg: by device model, by user account, by subscription type).
	- Server add/remove registration token to the corresponding group → send message to that group.
See. [Details](https://firebase.google.com/docs/cloud-messaging/device-group#rest)