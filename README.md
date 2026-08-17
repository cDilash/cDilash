<p align="center">
  <img src="./assets/profile-header.svg" alt="Dilash — independent product engineer building mobile training apps" width="100%" />
</p>

<p align="center">
  <a href="https://www.everlift.fit"><img src="https://img.shields.io/badge/EVERLIFT-LIVE-4ADE80?style=for-the-badge&labelColor=0A111B" alt="Everlift website" /></a>
  <a href="https://apps.apple.com/us/app/everlift-gym-workout-log/id6760033237"><img src="https://img.shields.io/badge/APP_STORE-F7FAFC?style=for-the-badge&logo=apple&logoColor=F7FAFC&labelColor=0A111B&color=24303D" alt="Everlift on the App Store" /></a>
  <a href="https://play.google.com/store/apps/details?id=com.everlift.app"><img src="https://img.shields.io/badge/GOOGLE_PLAY-F7FAFC?style=for-the-badge&logo=googleplay&logoColor=F7FAFC&labelColor=0A111B&color=24303D" alt="Everlift on Google Play" /></a>
</p>

I build training apps for iOS and Android, solo — design, code, localization, store listings. Two of them are real: one is on both stores, the other I use every morning and still find bugs in.

Most of what I work on is local-first. I'd rather an app be useful on a plane than have a clever backend.

---

## 01 / Everlift

**[everlift.fit](https://www.everlift.fit)** · [App Store](https://apps.apple.com/us/app/everlift-gym-workout-log/id6760033237) · [Google Play](https://play.google.com/store/apps/details?id=com.everlift.app) · [Case study](https://github.com/cDilash/everlift-showcase)

<table>
<tr>
<td width="62%" valign="top">

A gym workout tracker. 752 commits since January 2026, still shipping — the most recent one was a QR redirect straight to the store listing.

The constraint everything else got built around: **logging a set has to be faster than the rest between sets.** If you're mid-set and the app takes six taps, you stop using it by week three. That decision is why the analytics live two screens deep instead of on the home tab, and why there's no account signup — the first launch drops you straight into a workout.

414 exercises. Nine languages — German, English, Spanish, French, Japanese, Korean, Portuguese (BR), Russian, Simplified Chinese — which was by far the most tedious part and the thing I'd budget three times as long for next time.

No ads, no subscription wall on the core logger.

</td>
<td width="38%" align="center" valign="middle">
  <a href="https://github.com/cDilash/everlift-showcase">
    <img src="https://www.everlift.fit/screenshots/01_home.png" alt="Everlift home screen" width="235" />
  </a>
</td>
</tr>
</table>

---

## 02 / Gati

**[Repository](https://github.com/cDilash/Gati)** — marathon coaching, 129 commits, not on any store. I'm the only user.

<table>
<tr>
<td width="38%" align="center" valign="middle">
  <img src="./assets/gati-recovery.png" alt="Gati recovery screen" width="235" />
</td>
<td width="62%" valign="top">

Gemini writes my training week; a plain math layer decides whether it's allowed to.

The opinion the whole app is built on: **a model should never author more than seven days of training at once.** I built the 18-week version first and deleted it. It generated a plan for week 14 based on data from week 1 that hadn't happened yet, and then had no honest way to revise it. Now it plans one week at a time from the check-in I actually filled in, and nothing beyond that exists.

The safety validator is about fifty lines and silently clamps whatever the model returns: 15% max week-over-week volume increase, long run capped at 35% of weekly volume, quality work at 20%, peak never above 1.6× where you started, taper at 75/50/30. The AI proposes. The arithmetic has veto.

Reads 48 health fields from Garmin every five minutes through a Supabase edge function, and pulls run history from Strava.

**Known broken:** the coach can move a workout but not add one — `NOT NULL constraint failed: workout.day_of_week`. It's been broken for a while and I keep not fixing it.

</td>
</tr>
</table>

<table>
<tr>
<td width="25%" align="center" valign="top">
  <img src="./assets/gati-today.png" alt="Gati Today screen" width="200" />
  <br /><sub><b>TODAY</b></sub>
</td>
<td width="25%" align="center" valign="top">
  <img src="./assets/gati-plan.png" alt="Gati Plan screen" width="200" />
  <br /><sub><b>PLAN</b></sub>
</td>
<td width="25%" align="center" valign="top">
  <img src="./assets/gati-coach.png" alt="Gati Coach chat" width="200" />
  <br /><sub><b>COACH</b> — chat that edits the plan</sub>
</td>
<td width="25%" align="center" valign="top">
  <img src="./assets/gati-runs.png" alt="Gati Runs list" width="200" />
  <br /><sub><b>RUNS</b></sub>
</td>
</tr>
</table>

---

## 03 / Bugs that took longer than they should have

A more honest signal than a tech-stack list.

- **Step counts were exactly half of what Apple Health reported.** I'd set the aggregation period to 60 minutes — hourly — and was reading it as daily. Two days of staring at a factor I assumed was a unit conversion.
- **A UTC timezone bug across ten files.** Workouts were being marked complete on the wrong day for anyone not on UTC, including me. The fix touched ten files because I'd been calling `new Date()` in ten places instead of once.
- **Gati's auto-skip was eating that morning's run.** It swept past workouts on launch, before the Strava sync had finished — so a run you'd just finished got marked skipped. Fixed by ordering the sweep after the sync and adding a 12-hour buffer.
- **Everlift and Gati both wanted Metro on port 8081.** Gati's binary happily downloaded Everlift's JavaScript bundle and died on `PlatformConstants could not be found`. Nothing warns you; the two dev servers just quietly poison each other.

---

## 04 / Also on here

**[Echofy](https://github.com/cDilash/Echofy)** — local Whisper transcription, nothing leaves the machine.

**[Load Balancer](https://github.com/cDilash/Load-Balancer-Game-Server)** — round-robin game-server balancer in Python, with real-time metrics. Older, and it shows, but the visualizations still hold up.

**[everlift-showcase](https://github.com/cDilash/everlift-showcase)** — the engineering write-up for Everlift, since the app source is private.

<p align="center">
  <a href="https://www.everlift.fit">everlift.fit</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/cDilash?tab=repositories">all public work</a>
</p>
