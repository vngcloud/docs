# Retention Policy

A retention policy helps you clean up old artifacts in a Repository automatically. You set rules to choose which artifacts to keep; vCR deletes the rest on a schedule or when you click **Run now**.

This feature suits teams whose CI pushes many tags (for example, one new tag per commit) and who want to control storage usage and quota cost.

{% hint style="warning" %}
Artifacts deleted by a retention policy **cannot be restored**. Always use **Dry run** to check before a real run or before you set a schedule.
{% endhint %}

## What is a retention policy

A retention policy is a set of rules that decide which artifacts in a repository are **kept**. When the policy runs, every in-scope artifact that no enabled rule keeps is **permanently deleted**.

Each repository has at most **one** retention policy. It has up to **15 rules** and **one schedule**. A repository without a policy shows an empty rule list and the schedule **None**.

Without a policy, every image you push is kept forever. Old build tags pile up, take up storage, and count toward the repository quota.

**Terms used on the portal**

| Term | Meaning | Example |
| --- | --- | --- |
| Repository | Your repository on vCR, the billing unit | `my-team` |
| Image | One image name in the repository | `my-team/backend` |
| Artifact | One pushed version of an image, identified by its digest (it can have one or more tags, or no tag) | `backend@sha256:ab12…` |
| Tag | A name that points to an artifact | `v1.4.2`, `latest` |
| Untagged artifact | An artifact with no tags left, usually created when you push over an existing tag | — |

## How rules work

Each rule is evaluated on its own, then the results are combined: **an artifact is kept if at least one enabled rule keeps it.** An artifact that no rule keeps is deleted. Disabled rules are ignored.

Each rule has 3 parts:

1. **Images** — *matching* or *excluding* a pattern. This part selects the images the rule looks at.
2. **Retain condition** — one of the templates below, with a number from 0 to 10000.
3. **Tags** — *matching* or *excluding* a pattern, plus the **Include untagged artifacts** checkbox.

| Template (as shown on the portal) | Keeps |
| --- | --- |
| retain the most recently pushed N artifacts per image | The N newest pushed artifacts, counted per image |
| retain the most recently pulled N artifacts per image | The N most recently pulled artifacts, counted per image |
| retain the artifacts pushed within the last N days | Artifacts pushed in the last N days |
| retain the artifacts pulled within the last N days | Artifacts pulled in the last N days |
| retain always | Every artifact the rule matches (no number needed) |

**Patterns**

* `**` matches everything, `*` matches any string of characters, `?` matches exactly one character.
* Use commas to enter several values: `backend,frontend` or `v1.*,release-*`.
* Allowed characters: letters, digits and `. _ - / * ? { } , [ ]`, up to 255 characters. The pattern cannot be empty.

**The number 0.** If you enter 0, the rule keeps no artifacts. Every matching artifact is deleted, unless another rule keeps it. The form shows a warning when you enter 0, for example: *Retain 0 most recently pushed artifacts: every matching artifact in each image will be deleted unless another rule retains it.* Use it with care.

**Images or tags outside every rule** are not touched by the policy. Only artifacts that a rule looks at (by image and tag pattern) can be deleted.

## How to use it on the portal

Go to **Container Registry → Repository list**, click a repository, then open the **Retention policy** tab (next to the Images, Users and History tabs). The tab has 3 sections: **Retention rules**, **Schedule** and **Retention runs**.

### Add a rule

1. Click **Add rule**. The **Add retention rule** dialog opens. It has 2 numbered sections.
2. **1. Select images** — in **For the images**, choose *matching* or *excluding*, then enter image names or a pattern (for example `**` for all images).
3. **2. Choose artifacts to keep**:
   * In **By artifact count or number of days**, choose a template and enter a number.
   * In **Tags**, choose *matching* or *excluding* and enter tags or a pattern.
   * Tick **Include untagged artifacts** if you want the rule to also look at untagged artifacts.
4. Click Save. The rule appears in the list as a sentence, for example: *For the images \*\*, retain the most recently pushed 10 artifacts per image with tags \*\* (excluding untagged artifacts).*

You cannot save two identical rules in the same repository.

### Edit, disable or delete a rule

Use the **Action** menu on the rule's row:

* **Edit** — change the rule.
* **Disable** / **Enable** — a disabled rule stays in the list with the status **Disabled**, but it is not used when the policy runs.
* **Delete** — remove the rule. A confirm dialog shows the rule before it is deleted.

### Set a schedule

1. In the **Schedule** section, click **Edit**.
2. Choose a schedule type:
   * **None** — runs only when you click Run now.
   * **Hourly** — every hour, at minute 0.
   * **Daily** — every day at 00:00 UTC (07:00 Vietnam time).
   * **Weekly** — every Sunday at 00:00 UTC (07:00 Vietnam time).
   * **Custom** — a 6-field cron expression in UTC: `second minute hour day-of-month month day-of-week`. Example: `0 0 2 * * *` runs at 02:00 UTC (09:00 Vietnam time). Runs must be at least 1 hour apart.
3. Save. The schedule applies to all rules of the repository.

The Schedule section shows the time in UTC and in your local time.

### Check with Dry run

A dry run applies all enabled rules to the repository exactly like a real run, but it **deletes nothing**. Use it to see in advance **which images** the rules touch, and **which artifacts (tags)** would be deleted or kept.

**Steps**

1. Click **Dry run**. A new row appears in **Retention runs** with **Dry run = Yes**.
2. Wait until the status changes to **Success**. The page refreshes every 10 seconds.
3. Click **Show tasks** on that row. Each image that the rules look at is one row (one task). Above the table you see: *Dry run: nothing was deleted. "Retained / Total" shows how many artifacts a real run would keep.*
4. Read the **Retained / Total** column for each image:

| Example | Meaning for a real run |
| --- | --- |
| `10 / 10` | This image loses no artifacts |
| `10 / 37` | 10 artifacts are kept, **27 artifacts would be deleted** |
| `0 / 12` | **All 12 artifacts would be deleted**. Check your rules again (for example a count of 0, or a tag pattern that is too narrow) |

5. Click **Log** on an image to see exactly **which artifacts and tags** would be deleted or kept (see below).

An image that is not in the task list is outside the scope of every rule, so it is not touched.

{% hint style="info" %}
Run a dry run again every time you add, edit, enable or disable a rule, and always before you click **Run now** or set a schedule. A real run gives the same result as the dry run if no artifacts are pushed or pulled between the two runs.
{% endhint %}

### View the retention log on the vCR portal

You can read the detailed log of each image directly on the vCR portal; you do not need Harbor. Logs are available for **Dry run**, **Run now** and **Schedule** runs.

1. In **Retention runs**, click **Show tasks** on the run you want to check.
2. Click **Log** on the image's row. The **Retention log of image &lt;image name&gt;** window opens.

The log starts with a header that shows the repository, how rules are combined, and whether the run is a dry run (`Dry Run: true`). Then it shows a table with one row per artifact. The main columns are:

| Column | Meaning |
| --- | --- |
| Digest | The digest of the artifact |
| Tag | The tags of the artifact (empty for an untagged artifact) |
| PushedTime / PulledTime | The last push / pull time, used by the push / pull templates |
| Retention | The result: `RETAIN` = kept, `DEL` = deleted (or would be deleted in a dry run), `ERR` = deletion failed |

Example log of a dry run:

```
Run retention process.
 Repository: my-team/backend
 Rule Algorithm: or
 Dry Run: true
+-----------------+--------+-------+--------+---------------------+---------------------+---------------------+-----------+
|     DIGEST      |  TAG   | KIND  | LABELS |     PUSHEDTIME      |     PULLEDTIME      |     CREATEDTIME     | RETENTION |
+-----------------+--------+-------+--------+---------------------+---------------------+---------------------+-----------+
| sha256:ab12...  | v1.4.2 | image |        | 2026/11/18 09:12:01 | 2026/11/19 02:00:13 | 2026/11/18 09:12:01 | RETAIN    |
| sha256:cd34...  | v1.4.1 | image |        | 2026/11/10 08:01:44 |                     | 2026/11/10 08:01:44 | DEL       |
| sha256:ef56...  |        | image |        | 2026/10/02 15:30:10 |                     | 2026/10/02 15:30:10 | DEL       |
+-----------------+--------+-------+--------+---------------------+---------------------+---------------------+-----------+
```

{% hint style="warning" %}
**Notes about the log**

* Read the log on the vCR portal (Retention policy tab). Do not use the Harbor UI to view or edit the retention policy.
* In a dry run, `DEL` means the artifact **would** be deleted in a real run; nothing has been deleted yet.
* In a real run, a row with `ERR`, or a "Retention error for artifact" line, means that artifact was **not** deleted. The task can still show **Success**, but it also shows the warning *N artifact(s) failed to delete*.
* If the log is empty, the window shows **No log**. Wait until the run has finished, then open it again.
{% endhint %}

### Run now

Click **Run now**. The **Run retention policy now** dialog warns that artifacts not retained by any rule will be permanently deleted. You can click **Run now** to continue, or **Dry run** to check first.

{% hint style="info" %}
The **Run now** and **Dry run** buttons are disabled until the repository has at least one enabled rule.
{% endhint %}

### Track a run

The **Retention runs** table has these columns:

| Column | Meaning |
| --- | --- |
| Status | Pending, Scheduled, Running, Success, Stopped, Error or Failed |
| Dry run | Yes for a dry run, No for a real run |
| Execution type | Manual (you clicked a button) or Schedule |
| Start time | When the run started |
| Duration | Shown when the run has finished |

The page refreshes every 10 seconds while a run is in progress.

Click **Show tasks** to see one task per image, with its status, **Retained / Total**, start time and duration. Click **Log** on a task to read the retention log of that image.

**Failed deletions.** A task can show **Success** even when some artifacts could not be deleted. In this case the task shows the warning *N artifact(s) failed to delete*. Open the **Log** and look for lines with "Retention error for artifact" or **Retention = ERR** to see why.

### Abort a run

Click **Abort** on a running run and confirm. The run stops after a few seconds and changes to **Stopped**. If the run had already finished, its result is kept. Artifacts that were already deleted are not restored.

## Examples

| Goal | Rule setup | Result |
| --- | --- | --- |
| Keep the 10 newest builds of every image | Images matching `**` · retain the most recently pushed 10 artifacts per image · tags matching `**` | Each image keeps its 10 newest artifacts; older ones are deleted |
| Keep releases forever, clean up dev builds | Rule 1: images `**` · retain always · tags matching `v*,release-*`. Rule 2: images `**` · retain the artifacts pushed within the last 14 days · tags matching `**` | Release tags are never deleted; other tags are kept for 14 days |
| Delete only untagged artifacts | Rule 1: images `**` · retain the most recently pushed 0 artifacts per image · tags `**` + include untagged artifacts. Rule 2: images `**` · retain always · tags `**`, excluding untagged artifacts | All tagged artifacts are kept; untagged artifacts are deleted |
| Clean up only one image | Images matching `backend` · retain the most recently pushed 5 artifacts per image · tags `**` | Only `backend` is cleaned up; other images are not touched |
| Clean up all images except one | Images excluding `base` · retain the most recently pushed 5 artifacts per image · tags `**` | Every image except `base` is cleaned up |
| Keep what is still in use | Images `**` · retain the artifacts pulled within the last 30 days · tags `**` | Artifacts not pulled in the last 30 days are deleted |

{% hint style="info" %}
After you add or edit rules, run a **Dry run** and check the **Retained / Total** column before you set a schedule.
{% endhint %}

## Limits

| Item | Limit |
| --- | --- |
| Retention policies per repository | 1 |
| Rules per repository | 15 |
| Schedules per repository | 1 |
| Count / days in a rule | 0 to 10000 |
| Pattern length | 1 to 255 characters |
| Custom cron | 6 fields, UTC, runs at least 1 hour apart |
| Duplicate rules | Not allowed |

## FAQ

**Can I restore deleted artifacts?** No. Deleted artifacts cannot be restored. Always use Dry run first.

**Why does the schedule use UTC?** The registry runs on UTC time. Add 7 hours to get Vietnam time. The portal also shows the schedule in your local time.

**What happens when I delete a rule?** The rule is deleted right away. The next run uses only the remaining enabled rules.

**Can I set a schedule before I add rules?** Yes. But a run only deletes artifacts when there is at least one enabled rule, and Run now and Dry run need at least one enabled rule.

**Why does a task show Success but some artifacts are still there?** Some deletions may have failed. Look for the *failed to delete* warning on the task and read the **Log**. See [Track a run](#track-a-run).
