---
title: "I won kernelCTF for a day: the story of exp586"
date: 2026-07-30
categories: [security, kernelctf]
tags: [kernelctf, linux-kernel, exploit-development, security-research, bug-bounty]
---

It took about 5.8 seconds, beat the next submission by 337 milliseconds, and made me the kernelCTF winner for one day. Then a 0-day became a 1-day and the result changed completely.

## Five seconds

After a lot of research, I had a working local privilege escalation exploit for the `lts-6.12.95` target. It used the vulnerability fixed by commit [`8173f7e2ce67e6ca1d4763f3da14e5b01ce77456`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=8173f7e2ce67e6ca1d4763f3da14e5b01ce77456), `rhashtable: clear stale iter->p on table restart`.

The exploit got `uid=0`, captured the flag, and submitted it to the kernelCTF form automatically.

I optimized the entire pipeline for speed:

- 11:59:59.007 UTC – target request started,
- 12:00:03.015 – VM console became available,
- 12:00:03.594 – exploit executed,
- 12:00:04.052 – root obtained,
- 12:00:04.055 – flag captured,
- 12:00:04.131 – form submitted,
- 12:00:04.758 – HTTP 2xx response received.


The exploit needed 461 milliseconds from execution to flag capture. The complete path from requesting the VM to getting the flag took 5.048 seconds. The full logged run took 5.751 seconds, or about 5.8 seconds.

Google's official timestamp for the submission was:

```text
2026-07-24T12:00:04.564Z
```

## The missing row

At first, my submission did not appear in the public spreadsheet, so `exp558` was shown as the winner.

I had a valid flag, an HTTP 2xx response, and a form confirmation, but no public row and no `expNNN` identifier. The organizers use two form-processing paths, and mine had not reached the public spreadsheet. Once they fixed that, it appeared as `exp586` and won the `lts-6.12.95` slot.

The next submission, `exp558`, had this timestamp:

```text
2026-07-24T12:00:04.901Z
```

The difference was exactly 337 milliseconds.

For about one day, it looked like I had won kernelCTF.

## The exp544 reclassification

The earlier `exp544` entry had originally appeared as a 0-day submission. It was later reclassified from 0-day to 1-day.

The classification changed because the vulnerability had already been disclosed on a public mailing list before it was exploited in kernelCTF. Under the kernelCTF rules, it therefore no longer qualified as a 0-day.

Changing the classification did not remove `exp544` from its original slot or change its priority for the vulnerability. But the patch commit added to the internal spreadsheet on July 21 did not appear in the public one.

That detail mattered. The kernelCTF rules tell researchers to check the public spreadsheet before submitting, both for slot availability and for duplicate vulnerabilities. When I submitted `exp586`, the public spreadsheet did not show that `exp544` had used exactly the same vulnerability.

After a manual correction, my result changed to:

```text
vuln dupe of exp544
```

![Public kernelCTF spreadsheet showing exp586 classified as a vulnerability duplicate of exp544](/commons/exp586.png)

The same vulnerability cannot be reused on the latest LTS target, even after the kernel version changes. The winning slot therefore went back to `exp558`.

## What was left

The duplicate label did not change the technical part: the exploit got root and captured a valid flag in 461 milliseconds. Submission was automatic, I had complete telemetry and reproducible artifacts, and I was still 337 milliseconds faster than the eventual winner.

In kernelCTF, old entries, the state of the public spreadsheet, and the organizer's final classification matter too.

At least for one day, I could say that I had won kernelCTF :D

## References

- [kernelCTF public spreadsheet](https://docs.google.com/spreadsheets/d/e/2PACX-1vS1REdTA29OJftst8xN5B5x8iIUcxuK6bXdzF8G1UXCmRtoNsoQ9MbebdRdFnj6qZ0Yd7LwQfvYC2oF/pubhtml#gid=2095368189)
- [kernelCTF rules](https://google.github.io/security-research/kernelctf/rules.html)
