# Incident Report: [Brief Title]

**Incident ID:** INC-[YYYY-MM-DD]-[ID]
**Severity:** [P1-Critical / P2-High / P3-Medium / P4-Low]
**Status:** [Investigating / Mitigating / Resolved / Closed]
**Incident Commander:** [Name]

---

## Executive Summary

[1-2 paragraph summary of what happened, impact, and resolution. This should be understandable by non-technical stakeholders.]

---

## Incident Timeline

### Detection
**Time:** [YYYY-MM-DD HH:MM UTC]
**Detected by:** [Monitoring system / User report / Team member]
**Detection method:** [Alert / Support ticket / Manual observation]

### Response Timeline

| Time (UTC) | Event | Action Taken | Result |
|-----------|-------|--------------|--------|
| HH:MM | Incident detected | Alert triggered | Team notified |
| HH:MM | Investigation started | [Action] | [Result] |
| HH:MM | Root cause identified | [Action] | [Result] |
| HH:MM | Mitigation deployed | [Action] | [Result] |
| HH:MM | Service restored | [Action] | [Result] |
| HH:MM | Incident resolved | [Action] | [Result] |

**Total Duration:** [X hours Y minutes]

---

## Impact Assessment

### User Impact
**Affected Users:** [Number or percentage]
**Affected Features:** [List of features/services]
**Degraded Functionality:** [What didn't work or worked poorly]

### Business Impact
**Revenue Impact:** $[X] (estimated)
**SLA Breach:** [Yes/No]
**Customer Complaints:** [Number]
**Support Tickets:** [Number]

### Technical Impact
**Systems Affected:**
- [System 1]
- [System 2]
- [System 3]

**Data Impact:**
- Data loss: [Yes/No] - [Details]
- Data corruption: [Yes/No] - [Details]
- Data inconsistency: [Yes/No] - [Details]

---

## Incident Details

### What Happened
[Detailed description of what went wrong, in chronological order]

1. [Event 1]
2. [Event 2]
3. [Event 3]

### Root Cause
**Primary Cause:**
[Detailed explanation of the root cause]

**Contributing Factors:**
- [Factor 1]
- [Factor 2]
- [Factor 3]

**Why It Wasn't Caught Earlier:**
[Explanation of why this slipped through]

### Technical Details
```
[Code snippets, logs, error messages, stack traces, or technical data]
```

**Relevant Logs:**
```
[2025-01-15 14:23:15] ERROR: Database connection timeout
[2025-01-15 14:23:16] ERROR: Failed to execute query
[2025-01-15 14:23:17] CRITICAL: Service unavailable
```

**System State:**
- CPU: [X]%
- Memory: [Y]GB
- Disk: [Z]%
- Network: [Status]

---

## Response Actions

### Immediate Mitigation
**Actions Taken:**
1. [Action 1] - By: [Name] - Time: [HH:MM]
2. [Action 2] - By: [Name] - Time: [HH:MM]
3. [Action 3] - By: [Name] - Time: [HH:MM]

**Effectiveness:**
- [Action 1]: [Effective/Partially effective/Ineffective]
- [Action 2]: [Effective/Partially effective/Ineffective]

### Permanent Fix
**Solution Implemented:**
[Description of the permanent fix]

**Code Changes:**
- PR: [Link]
- Commits: [List or link]
- Files changed: [List]

**Deployment:**
- Deployed to: [Production/Staging]
- Deployment time: [HH:MM UTC]
- Verification: [How it was verified]

### Communication
**Internal Communication:**
- [Time] - Notified: [Team/stakeholders]
- [Time] - Status update: [Summary]
- [Time] - All-clear: [Message sent]

**External Communication:**
- [Time] - Status page updated
- [Time] - Customer email sent
- [Time] - Social media update

---

## Prevention Measures

### Immediate Actions (Completed)
- [x] [Action 1] - Completed: [Date]
- [x] [Action 2] - Completed: [Date]

### Short-term Actions (Next 2 weeks)
- [ ] [Action 1] - Owner: [Name] - Due: [Date]
- [ ] [Action 2] - Owner: [Name] - Due: [Date]

### Long-term Actions (Next quarter)
- [ ] [Action 1] - Owner: [Name] - Due: [Date]
- [ ] [Action 2] - Owner: [Name] - Due: [Date]

### Monitoring Improvements
- [ ] Add alert for [specific condition]
- [ ] Improve dashboard to show [metric]
- [ ] Set up automated failover for [system]

### Process Improvements
- [ ] Update runbook for [scenario]
- [ ] Improve incident response procedure
- [ ] Schedule training on [topic]

---

## Lessons Learned

### What Went Well
1. [Positive aspect 1]
2. [Positive aspect 2]
3. [Positive aspect 3]

### What Could Be Improved
1. [Improvement area 1]
   - **Action:** [Specific improvement]
   - **Owner:** [Name]

2. [Improvement area 2]
   - **Action:** [Specific improvement]
   - **Owner:** [Name]

### Surprises / Unexpected Findings
- [Finding 1]
- [Finding 2]

### Where We Got Lucky
- [Lucky circumstance 1]
- [What could have made it worse]

---

## Metrics

### Response Metrics
| Metric | Target | Actual | Met? |
|--------|--------|--------|------|
| Time to Detect | < 5 min | [X] min | ✅/❌ |
| Time to Acknowledge | < 2 min | [Y] min | ✅/❌ |
| Time to Mitigate | < 30 min | [Z] min | ✅/❌ |
| Time to Resolve | < 2 hours | [A] hours | ✅/❌ |

### SLA Impact
- **SLA Target:** [X]% uptime
- **Actual This Month:** [Y]%
- **SLA Met:** [Yes/No]
- **Credits Owed:** $[Amount]

---

## Related Issues

- **Related Incidents:** [INC-XXX, INC-YYY]
- **Related Issues:** [Issue #123, Issue #456]
- **Related PRs:** [PR #789]
- **Related Alerts:** [Alert links]

---

## Follow-up Items

### Action Items
- [ ] **[Action 1]** - Owner: [Name] - Due: [Date] - Priority: [High/Medium/Low]
- [ ] **[Action 2]** - Owner: [Name] - Due: [Date] - Priority: [High/Medium/Low]
- [ ] **[Action 3]** - Owner: [Name] - Due: [Date] - Priority: [High/Medium/Low]

### Documentation Updates
- [ ] Update runbook: [Link]
- [ ] Update architecture docs
- [ ] Update monitoring playbook
- [ ] Create knowledge base article

### Review Schedule
- **1-week follow-up:** [Date] - Verify short-term actions completed
- **1-month follow-up:** [Date] - Review effectiveness of changes
- **Quarterly review:** [Date] - Long-term prevention measures

---

## Appendices

### Appendix A: Detailed Logs
```
[Full logs if needed]
```

### Appendix B: Code Changes
```diff
[Relevant code diffs]
```

### Appendix C: Monitoring Screenshots
[Screenshots of dashboards, alerts, etc.]

### Appendix D: Communication Templates
[Email templates, status page updates used]

---

## Approval

**Reviewed by:**
- [ ] Incident Commander: [Name] - Date: [YYYY-MM-DD]
- [ ] Tech Lead: [Name] - Date: [YYYY-MM-DD]
- [ ] Engineering Manager: [Name] - Date: [YYYY-MM-DD]
- [ ] Product Owner: [Name] - Date: [YYYY-MM-DD]

**Status:** [Draft / Under Review / Approved]

---

## Severity Classification Reference

**P1 - Critical:**
- Complete service outage
- Data loss or corruption
- Security breach
- Revenue-impacting issue

**P2 - High:**
- Major feature degradation
- Significant performance impact
- Affects large number of users

**P3 - Medium:**
- Minor feature degradation
- Affects small number of users
- Workaround available

**P4 - Low:**
- Minimal user impact
- Non-critical functionality
- Cosmetic issues

---

*Report created: [YYYY-MM-DD]*
*Last updated: [YYYY-MM-DD]*
*Incident closed: [YYYY-MM-DD]*
