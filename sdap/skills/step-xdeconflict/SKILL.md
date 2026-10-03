---
name: step-xdeconflict
description: S6. Check that the domains fit each other across the interfaces from S3. The expensive gate.
---
# S6 - Cross-domain deconflict
Input: all domain specs + the interface list from `spec/allocation.md`.
Do: verify each interface agrees - voltage levels, current draw, physical fit, timing, thermal.
Output: an interface-agreement report.
Gate passes when: every interface from S3 is consistent. On a mismatch, rollback to the
owning S4 spec (`to=S4`, name the domain). This catches the bug class that otherwise only
appears at final assembly - the most expensive place to find it.
