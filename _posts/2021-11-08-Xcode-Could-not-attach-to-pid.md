---
layout: post
title:  "How to fix Xcode  Could not attach to pid Error"
date:   2021-11-08 16:53:24 +0800
categories: xcode kb
---

While i was debug a desktop app on xcode, then an error popup:
`Xcode: Could not attach to pid : “xxxx”`

more hint of this error is:
```
attach failed (Not allowed to attach to process.  Look in the console messages (Console.app), near the debugserver entries, when the attach failed.  The subsystem that denied the attach permission will likely have logged an informative message about why it was denied.)
Details
Could not attach to pid : “xxxx”
Domain: IDEDebugSessionErrorDomain
Code: 3
Failure Reason: attach failed (Not allowed to attach to process.  Look in the console messages (Console.app), near the debugserver entries, when the attach failed.  The subsystem that denied the attach permission will likely have logged an informative message about why it was denied.)
User Info: {
    DVTRadarComponentKey = 855031;
    IDERunOperationFailingWorker = DBGLLDBLauncher;
    RawUnderlyingErrorMessage = "attach failed (Not allowed to attach to process.  Look in the console messages (Console.app), near the debugserver entries, when the attach failed.  The subsystem that denied the attach permission will likely have logged an informative message about why it was denied.)";
}
System Information
macOS Version 11.6 (Build 20G165)
Xcode 13.1 (19466) (Build 13A1030d)
```

**My solution is as follows, set the Xcode settings:**
```bash
TARGETS -> Build Settings -> Signing -> 
Code signing inject base entitlements  : Yes
```
