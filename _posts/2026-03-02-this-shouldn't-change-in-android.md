---
title: This Shouldn't Change in Android
date: 2026-03-02 10:30:00 +0530
categories: [Android Notes]
tags: [android, practices]
---

Recently, while working on a new build flavor for a client that required a separate Play Store release, I asked for a new `applicationId`. The response was: *“Use the same one we use for the main app.”*

That triggered a discussion around why a new app needs:
- A separate package name (`applicationId`)
- A separate signing certificate

Changing either means it is no longer the same app in the eyes of Android.

While thinking more about this, I revisited an old but gold article by Dianne Hackborn:
“Things That Cannot Change” (2011). 

(blog link)[https://android-developers.googleblog.com/2011/06/things-that-cannot-change.html]

Even though it’s old, the principle remains absolutely relevant.

---

## The Core Principle

After listing everything that shouldn’t change, I realized they all follow one fundamental rule:

- Anything externally visible becomes a **contract**
- Contracts cannot change without migration
- If you must change them, you need a backward compatibility plan

---

## Things That Should Not Change (Lightly)

### 1. App Identity
- `applicationId` (package name)
- Signing certificate

Changing either creates a new app:
- No upgrade path
- No shared data
- Different Linux UID

These are permanent.

---

### 2. Manifest-Declared Public Components

If exported, they are public API:
- Activities
- Services
- BroadcastReceivers
- ContentProviders
- Deep links
- Launcher activity
- Widget providers
- Accessibility services

Renaming or removing them can break:
- Shortcuts
- PendingIntents
- Widgets
- External integrations

---

### 3. Intent Contracts
- Intent action strings
- Extra keys
- Deep link paths

If other modules, apps, or the system depend on them, they become stable API.

---

### 4. ContentProvider Authority

Authority string must remain stable.
Changing it breaks:
- FileProvider URIs
- Shared content
- Existing references

---

### 5. Database Schema (Without Migration)

User data is sacred.

Changing schema without proper migration:
- Crashes on update
- Data loss

---

### 6. SharedPreferences Keys

Renaming keys without migration causes silent logical failures.

---

### 7. Notification Channel IDs (Android 8+)

Once created:
- Importance cannot change
- Changing ID creates a new channel
- User settings are lost

---

### 8. Anything Persisted or OS-Registered

If it is:
- Stored on disk
- Saved in state
- Registered with the system
- Referenced by another app

Treat it as immutable.

---

## Mental Model

Everything inside your module is flexible.  
Everything outside your module is a contract.

As an Android developer, maturity comes from recognizing which side you’re modifying.

If it crosses a boundary:
- Version it
- Migrate it
- Or don’t change it

---

Most production bugs during app updates come from breaking contracts — not from business logic errors.
