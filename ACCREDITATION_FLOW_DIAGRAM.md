# Accreditation Flow Diagram
## Visual Workflow for US Investor Compliance

```
US INVESTOR CONNECTS WALLET
          ↓
    KYC VERIFICATION
    (Redbelly Network)
          ↓
   ╔═══════════════════════════════════════╗
   ║        ACCREDITATION CHECK            ║
   ║    (30-day deadline created)          ║
   ╚═══════════════════════════════════════╝
          ↓
    ┌─────────────────────────────────────────┐
    │               THREE PATHS               │
    └─────────────────────────────────────────┘
          ↓
    ┌─────┬─────────┬─────────────────────────┐
    │  A  │    B    │           C             │
    │     │         │                         │
    ▼     ▼         ▼                         ▼
┌─────┐ ┌───┐ ┌─────────────┐ ┌─────────────────────┐
│30-DAY│ │ADM│ │MANUAL ADMIN │ │DOCUMENT UPLOAD      │
│PROCESS│ │IN │ │OVERRIDE ⭐  │ │PORTAL (V2) 🚀      │
│       │ │   │ │             │ │                     │
│investr│ │OVE│ │• Form D     │ │• Self-upload        │
│ready. │ │RRI│ │• CPA Letter │ │• Admin review       │
│com    │ │DE │ │• Existing   │ │• 2-3 day process   │
│       │ │   │ │  proof      │ │                     │
│       │ │   │ │• INSTANT    │ │                     │
│       │ │   │ │  APPROVAL   │ │                     │
└─────┘ └───┘ └─────────────┘ └─────────────────────┘
    │     │         │                         │
    ▼     ▼         ▼                         ▼
┌─────────────────────────────────────────────────┐
│              INVESTMENT PHASE                   │
│                                                 │
│  ✅ ACCREDITED: Can invest without restrictions│
│  ⏳ PROVISIONAL: Can invest during grace period│
│  ❌ EXPIRED: Investments auto-cancelled        │
└─────────────────────────────────────────────────┘
          ↓
    ╔═══════════════════════════════════════╗
    ║         BACKGROUND MONITORING         ║
    ║                                       ║
    ║  • Scheduler runs every 6 hours       ║
    ║  • Checks accreditation deadlines     ║
    ║  • Auto-cancels expired investments   ║
    ║  • Refunds principal only             ║
    ║  • Sends notifications                ║
    ╚═══════════════════════════════════════╝
```

## Admin Manual Override Process ⭐ NEW

```
INVESTOR HAS EXISTING DOCUMENTATION
          ↓
    CONTACTS ADMIN/SUPPORT
          ↓
┌─────────────────────────────────────────┐
│        ADMIN VERIFICATION               │
│                                         │
│  • Reviews Form D filing                │
│  • Validates CPA accreditation letter   │
│  • Confirms previous investment proof    │
│  • Verifies document authenticity       │
└─────────────────────────────────────────┘
          ↓
    API CALL: approve-accreditation
    {
      "adminId": 1,
      "documentationType": "Form D Filing",
      "documentationNotes": "SEC Form D from 2024 investment",
      "bypassReason": "Existing accreditation verification"
    }
          ↓
    ╔═══════════════════════════════════════╗
    ║           INSTANT APPROVAL            ║
    ║                                       ║
    ║  ✅ isAccredited: true                ║
    ║  🗑️ accreditationDeadline: null       ║
    ║  📝 Audit trail created               ║
    ║  📧 Investor notification sent        ║
    ╚═══════════════════════════════════════╝
          ↓
    INVESTOR CAN INVEST IMMEDIATELY
```

## Notification Timeline ⭐ NEW

```
DAY 0: Investment Interest
  ↓
  📧 "Complete accreditation within 30 days"
  
DAY 3: First Reminder  
  ↓
  📧 "27 days remaining for accreditation"
  
DAY 6: Regular Check
  ↓
  📧 "24 days remaining for accreditation"
  
DAY 23: Urgent Warning
  ↓
  🚨 "7 days remaining - urgent action needed"
  
DAY 27: Critical Alert
  ↓
  ⚠️ "3 days remaining - investment at risk"
  
DAY 30: Deadline Expired
  ↓
  ❌ Investment automatically cancelled
  💰 Principal refunded (no interest)
  📧 Cancellation notification sent
```

## Investment Status Flow

```
US INVESTOR WORKFLOW STATES:

┌─────────────┐    KYC     ┌──────────────┐
│   WALLET    │─────────→  │   VERIFIED   │
│  CONNECTED  │            │     USER     │
└─────────────┘            └──────────────┘
                                  │
                            Accreditation
                              Check
                                  ▼
                           ┌──────────────┐
                           │ PROVISIONAL  │◄──┐
                           │   STATUS     │   │
                           └──────────────┘   │
                                  │           │
                          ┌───────┴───────┐   │
                          │               │   │
                        SUCCESS        TIMEOUT
                          │               │   │
                          ▼               ▼   │
                   ┌──────────────┐ ┌─────────┤
                   │ ACCREDITED   │ │CANCELLED│
                   │    USER      │ │INVESTMENT│
                   └──────────────┘ └─────────┘
                          │
                    Can Invest
                     Freely
                          ▼
                   ┌──────────────┐
                   │   ACTIVE     │
                   │ INVESTMENT   │
                   └──────────────┘
```

## Admin Dashboard Views ⭐ NEW

```
ADMIN MONITORING INTERFACE:

┌─────────────────────────────────────────────────┐
│               APPROACHING DEADLINES             │
├─────────────────────────────────────────────────┤
│  User ID │ Address     │ Days Left │ Status     │
│  1001    │ 0x1234...   │    3      │ URGENT     │
│  1002    │ 0x5678...   │    7      │ WARNING    │
│  1003    │ 0x9abc...   │   14      │ PENDING    │
└─────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────┐
│               MANUAL APPROVALS                  │
├─────────────────────────────────────────────────┤
│  [Approve User 1001]  Document: Form D         │
│  [Approve User 1005]  Document: CPA Letter     │
│  [Approve User 1010]  Document: Previous Proof │
└─────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────┐
│             RECENT CANCELLATIONS                │
├─────────────────────────────────────────────────┤
│  User 1008: $10,000 investment cancelled       │
│  User 1012: $25,000 investment cancelled       │
│  User 1015: $5,000 investment cancelled        │
│  Total Refunded: $40,000 (principal only)      │
└─────────────────────────────────────────────────┘
```

This visual workflow demonstrates the complete accreditation compliance system with emphasis on the new manual override capability and automatic enforcement features.