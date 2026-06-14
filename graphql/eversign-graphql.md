# Eversign GraphQL Schema

## Overview

This GraphQL schema models the Eversign (Xodo Sign) e-signature REST API. Eversign provides a RESTful JSON API for creating and sending documents for electronic signature, managing templates, uploading files, tracking audit trails, bulk sending via CSV, and receiving webhook event notifications for document lifecycle events.

## Provider

- **Name**: Eversign
- **Base URL**: https://api.eversign.com
- **Documentation**: https://eversign.com/api/documentation
- **GitHub**: https://github.com/eversign

## Schema Source

This schema was derived from the Eversign REST API documentation at https://eversign.com/api/documentation. The schema captures the core data structures used across:

- Document creation, sending, and lifecycle management
- Template creation and use
- Signer and recipient management
- Form field definitions and values
- File uploads and retrieval
- Audit trail tracking
- Reminder and expiry configuration
- Business and team member management
- OAuth applications and API key management
- Webhook event handling

## Types

### Document Types
- `Document` — Core document entity with all fields
- `DocumentDetails` — Detailed view of a document including full signer and field lists
- `DocumentStatus` — Status enum (draft, sent, completed, cancelled, declined, expired)
- `DocumentMessage` — Email message attached to a document send
- `DocumentTitle` — Document title wrapper

### Template Types
- `Template` — Template entity for reusable document definitions
- `TemplateDetails` — Full template details including roles and fields
- `TemplateTitle` — Template title wrapper

### Signer Types
- `Signer` — Entity representing a document signer
- `SignerDetails` — Extended signer info including status and signature timestamp
- `SignerRole` — Role definition used in templates
- `SignerOrder` — Ordering configuration for sequential signing
- `SignerMessage` — Custom message for a specific signer

### Signature Types
- `Signature` — A completed signature record
- `SignatureDetails` — Extended signature record with image and metadata
- `SignatureDate` — Date/time of signature capture

### Form Field Types
- `FormField` — A single form field placed on a document
- `FormFieldDetails` — Extended form field with value and validation info
- `FormFieldType` — Enum of supported field types (signature, initials, date, text, checkbox, etc.)
- `FormFieldValue` — Value captured for a form field after signing

### Recipient Types
- `Recipient` — Entity that receives a document (signer or CC)
- `RecipientDetails` — Extended recipient info with delivery status
- `RecipientEmail` — Email address wrapper for a recipient
- `RecipientCC` — Carbon-copy recipient who receives a copy but does not sign

### File Types
- `File` — File metadata associated with a document
- `FileDetails` — Extended file info with page count and dimensions
- `FileURL` — Remote URL used to fetch a file
- `FileBase64` — Base64-encoded file content for inline upload

### Audit Trail Types
- `AuditTrail` — Complete audit trail for a document
- `AuditEntry` — Single audit trail event record
- `AuditEntryType` — Enum of audit event types (created, sent, viewed, signed, declined, etc.)

### Reminder and Expiry Types
- `Reminder` — Reminder configuration for a document
- `ReminderDetails` — Extended reminder with frequency and last-sent info
- `Expiry` — Expiry configuration for a document
- `ExpiryDate` — Specific expiry date/time value

### Business Types
- `Business` — Business account entity
- `BusinessDetails` — Extended business info with plan and usage
- `BusinessAddress` — Physical address for a business

### Team Types
- `TeamMember` — A member of a business team
- `MemberDetails` — Extended member info with permissions
- `MemberRole` — Role enum for team members (admin, member, viewer)

### Auth Types
- `OAuthApp` — An OAuth application registered with Eversign
- `APIKey` — API key credential
- `Token` — OAuth access/refresh token pair

### Webhook Types
- `Webhook` — Registered webhook endpoint
- `WebhookEvent` — A webhook event payload delivered to an endpoint

### Error Types
- `Error` — General API error response
- `ValidationError` — Field-level validation error with path and message

## Usage Notes

- All document and template queries require a valid `access_key` (API key) or OAuth bearer token.
- Business ID (`business_id`) is required for most mutations involving documents and templates.
- File uploads support both remote URL (`FileURL`) and base64 inline (`FileBase64`) modes.
- Audit trails are immutable once recorded.
- Webhook payloads use `WebhookEvent` and reference the associated `Document` by hash ID.
