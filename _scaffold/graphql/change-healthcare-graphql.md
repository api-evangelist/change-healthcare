# Change Healthcare GraphQL Schema

## Overview

This conceptual GraphQL schema represents the Change Healthcare (now part of Optum/UnitedHealth Group) healthcare transaction and data platform. Change Healthcare operates as one of the largest health information networks in the United States, processing billions of healthcare transactions annually including eligibility verifications, claim submissions, prior authorizations, and remittance advice.

The schema covers the full healthcare administrative transaction lifecycle: from eligibility inquiry through claim submission, adjudication, remittance, and appeals.

## Provider Context

- **Provider**: Change Healthcare (Optum/UnitedHealth Group)
- **Platform**: Healthcare clearinghouse and transaction processing
- **Base URL**: https://api.changehealthcare.com
- **Developer Portal**: https://developers.changehealthcare.com/
- **GitHub**: https://github.com/changehealthcare
- **Primary Standards**: X12 EDI (270/271, 276/277, 278, 835, 837P/I/D), HL7, FHIR

## Schema Design

### Core Domains

**Parties and Identity**
- `Provider` - Rendering, billing, and referring providers identified by NPI
- `Payer` - Insurance payers with electronic payer IDs and clearinghouse codes
- `Patient` - The individual receiving healthcare services
- `Subscriber` - The insurance policy holder (may differ from patient)
- `Member` - The insured individual with plan and group information
- `PolicyHolder` - The employer or individual holding the policy

**Coverage and Benefits**
- `Eligibility` - Real-time eligibility inquiry and response (EDI 270/271)
- `Coverage` - Active insurance plan coverage details
- `EligibilityBenefit` - Specific benefit details by service type
- `Deductible` - Individual and family deductible tracking
- `Copay` - Fixed-dollar cost sharing by service type
- `Coinsurance` - Percentage-based cost sharing

**Claims**
- `Claim` - Healthcare claim (professional 837P, institutional 837I, dental 837D)
- `ClaimLine` - Individual service line on a claim
- `Diagnosis` - ICD-10/ICD-11 diagnosis codes
- `Procedure` - CPT/HCPCS procedure codes
- `ClaimStatusResponse` - Claim status inquiry response (EDI 276/277)

**Remittance and Payment**
- `ERA` - Electronic Remittance Advice (EDI 835)
- `EOB` - Explanation of Benefits
- `Remittance` - Aggregate payment and remittance information
- `PaymentAdvice` - EFT/check payment details
- `Adjustment` - Claim and line-level adjustments with reason codes
- `Denial` - Denial reasons with appeal deadline tracking

**Prior Authorizations and Referrals**
- `PriorAuth` - Prior authorization requests and decisions (EDI 278)
- `ReferralRequest` - Specialist referral requests
- `Appeal` - Denied claim appeal tracking
- `Attachment` - Clinical documentation attachments

**EDI and Clearinghouse**
- `InterchangeEnvelope` - X12 ISA/IEA interchange envelope
- `FunctionalGroup` - X12 GS/GE functional group
- `TransactionSet` - Individual X12 transaction sets
- `X12Batch` - Batch submission of X12 transactions
- `EDIFile` - Raw EDI file tracking
- `ValidationReport` - Pre-submission validation results
- `SubmissionResult` - Submission acknowledgment with accept/reject counts
- `RejectionReason` - Structured rejection codes and resolutions
- `ClearinghouseCode` - Clearinghouse-specific code definitions

**Administrative**
- `PayerList` - Searchable payer directory
- `FeeSchedule` - Payer-specific allowed amount schedules

## Type Summary

| Category | Types |
|---|---|
| Enumerations | ClaimType, ClaimFrequency, ClaimStatus, ServiceType, PlaceOfService, NetworkStatus, AuthorizationStatus, EligibilityStatus, GenderCode, TransactionSetType, ValidationSeverity |
| Core Parties | NPI, TaxId, Address, Provider, Payer, Patient, Subscriber, Member, PolicyHolder |
| Coverage | Eligibility, Coverage, EligibilityBenefit, Deductible, Copay, Coinsurance |
| Claims | Claim, ClaimLine, Diagnosis, Procedure, ClaimStatusResponse |
| Remittance | ERA, EOB, Remittance, PaymentAdvice, Adjustment, Denial |
| Authorizations | PriorAuth, ReferralRequest, Appeal, Attachment |
| EDI/X12 | InterchangeEnvelope, FunctionalGroup, TransactionSet, X12Batch, EDIFile, ValidationReport, ValidationIssue, SubmissionResult, RejectionReason, ClearinghouseCode |
| Administrative | PayerList, FeeSchedule |
| Input Types | AddressInput, ClaimInput, ClaimLineInput, EligibilityRequestInput, PriorAuthInput, ReferralInput, AppealInput, AttachmentInput |

**Total named types: 70+**

## Key Queries

```graphql
# Check real-time eligibility
query CheckEligibility {
  checkEligibility(
    memberId: "MBR123456"
    payerId: "00001"
    serviceDate: "2026-06-14"
    serviceTypes: [MEDICAL_CARE, PREVENTIVE]
  ) {
    status
    member {
      memberId
      patient { firstName lastName dateOfBirth }
    }
    benefits {
      serviceType
      copay { amount }
      deductible { individual individualMet }
    }
  }
}

# Submit a professional claim
mutation SubmitClaim {
  submitClaim(claim: {
    claimType: PROFESSIONAL
    claimFrequency: ORIGINAL
    patientId: "PAT001"
    subscriberId: "SUB001"
    renderingProviderNPI: "1234567890"
    billingProviderNPI: "0987654321"
    payerId: "00001"
    serviceStartDate: "2026-06-01"
    serviceEndDate: "2026-06-01"
    diagnosisCodes: ["Z00.00"]
    totalChargeAmount: 250.00
    claimLines: [{
      lineNumber: 1
      serviceDate: "2026-06-01"
      placeOfService: OFFICE
      procedureCode: "99213"
      quantity: 1
      chargeAmount: 250.00
      diagnosisPointers: ["1"]
    }]
  }) {
    transactionId
    status
    acceptedCount
    rejectedCount
    validationReport { isValid errors { code message } }
  }
}

# Get claim status
query ClaimStatus {
  getClaimStatus(claimNumber: "CLM2026001", payerId: "00001") {
    status
    statusDate
    checkDate
    paidAmount
    adjustmentReasonCodes
  }
}
```

## Standards Coverage

| EDI Transaction | Description | GraphQL Type |
|---|---|---|
| 270/271 | Eligibility Inquiry/Response | `Eligibility`, `EligibilityBenefit` |
| 276/277 | Claim Status Request/Response | `ClaimStatusResponse` |
| 278 | Prior Auth Request/Response | `PriorAuth`, `ReferralRequest` |
| 835 | Electronic Remittance Advice | `ERA`, `Remittance` |
| 837P | Professional Claim | `Claim` (ClaimType: PROFESSIONAL) |
| 837I | Institutional Claim | `Claim` (ClaimType: INSTITUTIONAL) |
| 837D | Dental Claim | `Claim` (ClaimType: DENTAL) |

## Notes

This is a conceptual schema derived from Change Healthcare's public developer documentation, API patterns, and standard healthcare EDI specifications. Change Healthcare operates primarily through REST APIs and EDI file exchange; this GraphQL schema represents the domain model that underlies those transactional services. The schema is intended for integration planning, data modeling, and tooling purposes.
