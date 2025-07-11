# Quick Reference: Accreditation System

## 🚀 What We Built Today

### V1 Manual Accreditation Override
**Purpose**: Handle investors with existing accreditation documentation
**Result**: Instant approval bypassing 30-day deadline

### API Endpoint
```bash
POST /api/admin/users/:userId/approve-accreditation
{
  "adminId": 1,
  "documentationType": "Form D Filing",
  "documentationNotes": "Details about existing proof", 
  "bypassReason": "Investor has SEC documentation"
}
```

### Automatic Investment Cancellation
**Purpose**: Enforce compliance for US investors
**Result**: Auto-cancel investments when accreditation deadline expires

## 📋 Complete US Investor Journey

1. **Connect Wallet** → Auto-detects US jurisdiction
2. **KYC Verification** → Mandatory Redbelly Network KYC  
3. **Accreditation Options**:
   - 📅 **Standard**: 30-day process via investready.com
   - ⚡ **Manual Override**: Admin approval with existing docs (NEW)
   - 📁 **Upload Portal**: Self-service (V2 planned)
4. **Investment** → Provisional during grace period
5. **Monitoring** → Smart notifications and deadline tracking
6. **Enforcement** → Automatic cancellation if deadline expires

## 🌍 Non-US Investor Journey  

1. **Connect Wallet** → Auto-detects Non-US jurisdiction
2. **KYC Verification** → Same Redbelly requirement
3. **Invest Immediately** → No accreditation needed
4. **Lower Minimums** → $100 vs $5,000 for US

## 🔧 Admin Tools

### Monitor Deadlines
```bash
GET /api/admin/accreditation/approaching-deadlines?days=7
```

### Manual Processing  
```bash
POST /api/admin/accreditation/process-deadlines
```

### Manual Approval
```bash
POST /api/admin/users/:userId/approve-accreditation
```

## 📊 Key Benefits

### For Investors
- ✅ Clear compliance path
- ✅ Multiple accreditation options  
- ✅ Provisional investing capability
- ✅ Smart deadline notifications

### For Admins
- ✅ Manual override capability
- ✅ Complete audit trail
- ✅ Automated enforcement
- ✅ Deadline monitoring tools

### For Platform
- ✅ Regulatory compliance
- ✅ Automatic risk management
- ✅ Scalable verification process
- ✅ Documentation tracking

## 🎯 V2 Roadmap

- **Document Upload Portal**: Investor self-service
- **Enhanced File Management**: Storage and versioning
- **OCR Validation**: Automatic document recognition
- **Audit Trail**: Complete history tracking