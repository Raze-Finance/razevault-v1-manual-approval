# RazeVault Investor Workflow Guide
## Complete User Experience for US and Non-US Investors

### Overview
RazeVault provides a comprehensive investment platform with strict regulatory compliance for both US and Non-US investors. This guide outlines the complete investor journey from wallet connection to investment redemption, with special emphasis on our accreditation verification system.

---

## 🇺🇸 US Investor Workflow

### Phase 1: Initial Setup & KYC
1. **Wallet Connection**
   - Connect wallet via Dynamic.xyz (supports social login)
   - System auto-detects US jurisdiction
   - Redirected to US-specific vault pages

2. **Mandatory KYC Verification**
   - Automatic redirect to `access.redbelly.network` if not KYC'd
   - Complete Redbelly Network KYC verification
   - Jurisdiction validation prevents circumvention
   - **Cannot proceed without KYC completion**

### Phase 2: Accreditation Verification ⭐ NEW
3. **Accreditation Status Check**
   - System creates 30-day accreditation deadline for new US investors
   - Three possible paths:

#### Path A: Standard 30-Day Process
- Redirect to `investready.com` for accreditation verification
- 30-day grace period for document submission
- Can make provisional investments during grace period
- **Automatic cancellation** if deadline expires without accreditation

#### Path B: Manual Admin Override ⭐ NEW (V1)
- Investor contacts admin with existing documentation
- Admin calls: `POST /api/admin/users/:userId/approve-accreditation`
- Provides documentation details:
  ```json
  {
    "adminId": 1,
    "documentationType": "Form D Filing / CPA Letter / etc",
    "documentationNotes": "Details about existing proof",
    "bypassReason": "Investor has SEC Form D from previous investment"
  }
  ```
- **Instant approval** - bypasses 30-day deadline completely
- Creates audit trail with admin ID, timestamp, documentation type
- Investor receives approval notification

#### Path C: Document Upload Portal (V2 Planned)
- Investor uploads accreditation proof directly
- Admin review queue (2-3 business days)
- Much faster than 30-day standard process

### Phase 3: Investment Process
4. **Currency Options**
   - Input: USDC/AVAX (familiar currencies)
   - Automatic conversion to USDT/RBNT on Redbelly Network
   - Platform handles cross-chain bridging seamlessly

5. **Yield Tier Selection**
   - 30-day lockup: 8% APR
   - 90-day lockup: 10% APR  
   - 365-day lockup: 12% APR
   - Minimum investment: $5,000 (regulatory compliance)

6. **Investment Validation**
   - System blocks investments from non-accredited users past deadline
   - Clear error messages if compliance not met
   - Provisional status during grace period

### Phase 4: Notification System ⭐ NEW
7. **Smart Deadline Tracking**
   - Initial accreditation reminder popup
   - 3-day interval reminders during grace period
   - Urgent warnings at 7 days remaining
   - Critical alerts at 3 days remaining
   - Dismissible banners with countdown timers

### Phase 5: Automatic Compliance ⭐ NEW
8. **Background Processing**
   - Scheduler runs every 6 hours checking deadlines
   - Automatic investment cancellation for expired deadlines
   - Principal-only refunds (no interest) for cancelled investments
   - Investment status changes from "provisional" to "cancelled"

---

## 🌍 Non-US Investor Workflow

### Phase 1: Initial Setup & KYC
1. **Wallet Connection**
   - Connect wallet via Dynamic.xyz
   - System auto-detects Non-US jurisdiction
   - Redirected to Non-US specific vault pages

2. **Mandatory KYC Verification**
   - Same Redbelly Network KYC requirement
   - Jurisdiction validation enforced
   - **Cannot proceed without KYC completion**

### Phase 2: Simplified Process
3. **No Accreditation Required**
   - Non-US investors skip accreditation verification
   - Can invest immediately after KYC
   - No 30-day waiting periods or deadlines

### Phase 3: Investment Process
4. **Currency Flow**
   - Uses USDT/RBNT throughout entire process
   - No cross-chain conversion needed
   - Direct investment on Redbelly Network

5. **Yield Tier Selection**
   - Same yield options as US investors
   - 30-day: 8% APR, 90-day: 10% APR, 365-day: 12% APR
   - Minimum investment: $100 (lower regulatory threshold)

---

## 🔧 Admin Management Tools ⭐ NEW

### Monitoring Dashboard
- `GET /api/admin/accreditation/approaching-deadlines?days=7`
- View investors approaching accreditation deadlines
- Filter by time remaining (7, 14, 30 days)
- Track compliance status across all users

### Manual Processing
- `POST /api/admin/accreditation/process-deadlines`
- Trigger deadline processing manually
- Review cancelled investments
- Monitor automatic compliance actions

### Manual Approval System
- Override 30-day deadlines for investors with existing documentation
- Complete audit trail with admin identification
- Instant accreditation approval capability
- Documentation type tracking (Form D, CPA letters, etc.)

---

## 🎯 Key Compliance Features

### Automatic Investment Cancellation ⭐ NEW
- **Trigger**: US investors who fail accreditation verification within 30 days
- **Action**: Investment automatically cancelled, principal refunded
- **Protection**: Prevents non-compliant investments from remaining active
- **Notification**: Investor informed of cancellation and refund

### Manual Override System ⭐ NEW  
- **Purpose**: Handle investors with existing accreditation documentation
- **Process**: Admin review of Form D filings, CPA letters, previous verifications
- **Result**: Instant approval bypassing standard 30-day process
- **Audit**: Complete tracking of who approved, when, and documentation basis

### Investment Validation
- **Prevention**: New investments blocked for non-compliant users past deadline
- **Grace Period**: Provisional investments allowed during 30-day verification window
- **Currency Separation**: US vs Non-US currency flows properly enforced
- **KYC Gates**: Universal Redbelly KYC requirement with jurisdiction validation

---

## 📊 User Experience Highlights

### For US Investors
✅ **Clear Path Forward**: Three distinct accreditation options
✅ **Provisional Investing**: Can invest during verification period  
✅ **Smart Notifications**: Proactive deadline reminders
✅ **Admin Support**: Manual override for existing documentation
✅ **Automatic Protection**: Compliance enforcement prevents violations

### For Non-US Investors  
✅ **Streamlined Process**: No accreditation complexity
✅ **Lower Minimums**: $100 vs $5,000 investment threshold
✅ **Immediate Access**: Invest right after KYC completion
✅ **Same Yields**: Equal return opportunities

### For Administrators
✅ **Monitoring Tools**: Track approaching deadlines
✅ **Manual Controls**: Override capability for special cases
✅ **Audit Trail**: Complete documentation of all approval decisions
✅ **Automated Compliance**: Background processing handles routine enforcement

---

## 🚀 V2 Roadmap

### Document Upload Portal
- Investor self-service document upload
- Admin review queue (2-3 day turnaround)
- OCR validation for common forms
- Version control and expiration tracking

### Enhanced Audit Trail
- Complete document history
- Timestamped access logs
- Multi-tenant document isolation
- Automated compliance reporting

This workflow ensures regulatory compliance while providing the best possible user experience for both investor types and administrative oversight.