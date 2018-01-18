---
title: "Restoring Lost Firefox Tabs"
date: 2018-01-14T17:42:00+01:00
draft: true
tags: ["firefox", "help"]
---

If you use the "Reopen tabs from last session" feature in Firefox, you might have a large interest in those tabs actually showing up after restarting it. If now you ever ran into the situation like me, that your tabs just were lost, here is how you might be able to restore them:

_Hint: This happens to me occasionally when using multiple windows. If you have opened your "main" window and in addition are using, e.g. private windows, then it is very crucial that the *last window you close is your main window*. Otherwise the "wrong" session will be restored - if any (in case of private windows)._

Firefox stores the information about your session in actually two places: `{PROFILE}\sessionstore.jsonlz4` and `{PROFILE}\sessionstore-backups\`. The first only is only existing when all your FF instances are closed. The latter one contains backups of the first file - but not that many. In my case it is one `previous`, one `recovery` and two additional ones which seem to be backups from five respectively 15 days ago.

When - in panically trying to find your lost tabs - you opened and closed FF multiple times, your `previous` and `recovery` most likely have been overwritten already. Then your only chances are

* Restoring them from your backup (which hopefully you have)
* Use one of the two older backups

Then just close your browser, copy the appropriate file to `{PROFILE}\sessionstore.jsonlz4`, and restart. Your tabs should appear again.