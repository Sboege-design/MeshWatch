# MeshWatch Product Specification Document

## Project Overview

**Project Name:** MeshWatch - A Peer-to-Peer ICE Activity Alert System  
**Version:** 1.0  
**Date:** July 2025  
**License:** MIT/GPL (TBD - Community Decision)  
**Repository:** [To be created]

### Mission Statement
Build a decentralized, Bluetooth-based mobile application that enables individuals in at-risk communities to report and receive localized alerts about ICE (Immigration and Customs Enforcement) activity without requiring cellular data, Wi-Fi, or central servers.

### Problem Statement
At-risk communities need a secure, offline-capable communication system to share time-sensitive information about enforcement activities. Current solutions rely on centralized infrastructure that can be monitored, disabled, or compromised, leaving vulnerable populations without reliable communication channels.

### Solution Overview
MeshWatch creates a peer-to-peer mesh network using Bluetooth Low Energy (BLE) technology, allowing users to broadcast and receive alerts within their immediate vicinity while maintaining complete anonymity and data sovereignty.

## Target Audience

### Primary Users
- **At-risk community members** in areas with high ICE activity
- **Community organizers** coordinating local safety efforts
- **Legal observers** documenting enforcement activities
- **Support network members** providing assistance to vulnerable populations

### Secondary Users
- **Civil rights organizations** requiring secure communication tools
- **Journalists** covering immigration enforcement
- **Legal aid providers** needing real-time community information

### User Personas

#### Persona 1: "Maria" - Community Member
- **Age:** 35
- **Background:** Undocumented immigrant, works multiple jobs
- **Tech comfort:** Basic smartphone usage
- **Needs:** Simple, secure way to receive warnings about ICE activity
- **Constraints:** Limited data plan, fears surveillance

#### Persona 2: "Carlos" - Community Organizer
- **Age:** 28
- **Background:** Legal resident, community advocate
- **Tech comfort:** Intermediate
- **Needs:** Coordinate community safety efforts, verify information
- **Constraints:** Needs to protect sources, maintain operational security

#### Persona 3: "Sarah" - Legal Observer
- **Age:** 42
- **Background:** Volunteer with legal aid organization
- **Tech comfort:** Advanced
- **Needs:** Document incidents, share verified information
- **Constraints:** Must maintain neutrality, protect witness identity

## Core Features & Requirements

### Phase 1: Minimum Viable Product (MVP)

#### Feature 1: Alert Creation
**Description:** Users can manually create and broadcast alerts about observed enforcement activity.

**Requirements:**
- Simple form with three fields: City, Street, Description
- Character limit: 280 characters for description
- No GPS or location services required
- Timestamp automatically added
- One-tap emergency clear function

**Acceptance Criteria:**
- User can input alert information in under 30 seconds
- Alert is immediately queued for Bluetooth broadcast
- Form validates required fields before submission
- No personally identifiable information is collected

#### Feature 2: Bluetooth Mesh Broadcasting
**Description:** Transmit alerts to nearby devices using Bluetooth Low Energy.

**Requirements:**
- Utilize Android Nearby Connections API or equivalent
- Broadcast range: 100-300 meters depending on device capabilities
- Message relay capability (mesh networking)
- Automatic device discovery and connection
- Encrypted message transmission

**Acceptance Criteria:**
- Messages successfully transmit to devices within range
- Relay functionality extends network reach
- Connection establishment takes less than 10 seconds
- Broadcast continues even when app is backgrounded

#### Feature 3: Alert Reception & Display
**Description:** Receive, store, and display incoming alerts from nearby devices.

**Requirements:**
- Real-time notification of new alerts
- Local storage in encrypted format
- Chronological display with timestamps
- Visual indicators for alert urgency/type
- Offline-first design

**Acceptance Criteria:**
- Alerts appear within 5 seconds of reception
- Notification system works when app is backgrounded
- Display clearly shows time, location, and description
- No internet connection required for core functionality

#### Feature 4: Message Expiry System
**Description:** Automatically delete alerts after 24 hours to protect user privacy.

**Requirements:**
- Configurable expiry timer (default: 24 hours)
- Automatic cleanup process
- Secure deletion of expired messages
- User notification of cleanup actions

**Acceptance Criteria:**
- Messages automatically delete after specified time
- Deletion process cannot be recovered
- User can manually adjust expiry settings
- Cleanup occurs without user intervention

#### Feature 5: Privacy & Security
**Description:** Ensure complete user anonymity and data protection.

**Requirements:**
- No user accounts or registration required
- No personal information collected or stored
- AES-256 encryption for stored messages
- End-to-end encryption for transmitted messages
- Panic mode for instant data deletion

**Acceptance Criteria:**
- App functions without any user identification
- All data encrypted at rest and in transit
- Panic mode clears all data in under 3 seconds
- No analytics or tracking implemented

### Phase 2: Enhanced Features (Future Development)

#### Multi-hop Mesh Networking
- Extended range through device-to-device relaying
- Intelligent routing algorithms
- Network topology optimization

#### Offline Mapping Integration
- OpenStreetMap integration for visual alerts
- Offline map caching
- Location-based alert filtering

#### Cross-Platform Compatibility
- iOS version using Multipeer Connectivity
- Platform-specific optimizations
- Shared protocol specification

#### Enhanced Security Features
- Optional PGP encryption layer
- Digital signatures for verified sources
- Advanced key management

## Technical Specifications

### Platform Requirements

#### Android (Primary Platform)
- **Minimum SDK:** Android 7.0 (API Level 24)
- **Target SDK:** Android 14 (API Level 34)
- **Architecture:** ARM64, x86_64
- **Permissions:** Bluetooth, Location (for BLE discovery only)

#### iOS (Phase 2)
- **Minimum Version:** iOS 13.0
- **Framework:** Multipeer Connectivity
- **Architecture:** ARM64

### Technology Stack

#### Core Technologies
- **Language:** Kotlin (Android), Swift (iOS)
- **Bluetooth:** Android Nearby Connections API, iOS Multipeer Connectivity
- **Database:** Room Database (Android), Core Data (iOS)
- **Encryption:** AES-256 for storage, TLS for transmission
- **UI Framework:** Jetpack Compose (Android), SwiftUI (iOS)

#### Dependencies
- **Networking:** Minimal external dependencies
- **Cryptography:** Built-in platform cryptography libraries
- **Storage:** Platform-native database solutions
- **Testing:** JUnit (Android), XCTest (iOS)

### Architecture Overview

#### High-Level Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   User Interface│    │  Business Logic │    │   Data Layer    │
│                 │    │                 │    │                 │
│ • Alert Creation│◄──►│ • Message Mgmt  │◄──►│ • Local Storage │
│ • Alert Display │    │ • Encryption    │    │ • Message Cache │
│ • Settings      │    │ • Validation    │    │ • User Prefs    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
                    ┌─────────────────┐
                    │ Bluetooth Layer │
                    │                 │
                    │ • Device Disc.  │
                    │ • Message Relay │
                    │ • Connection    │
                    │   Management    │
                    └─────────────────┘
```

#### Data Flow
1. User creates alert through UI
2. Business logic validates and encrypts message
3. Message stored locally and queued for broadcast
4. Bluetooth layer discovers nearby devices
5. Encrypted message transmitted to connected peers
6. Receiving devices decrypt and store message
7. Message displayed in recipient UI
8. Automatic cleanup after expiry period

### Security Architecture

#### Encryption Strategy
- **At Rest:** AES-256 encryption for local storage
- **In Transit:** End-to-end encryption using platform cryptography
- **Key Management:** Ephemeral keys, no persistent key storage
- **Authentication:** Message integrity verification

#### Privacy Protection
- **No User Tracking:** Zero analytics or user identification
- **Data Minimization:** Only essential data collected
- **Secure Deletion:** Cryptographic erasure of expired data
- **Network Isolation:** No internet connectivity required

#### Threat Model
- **Passive Surveillance:** Encryption prevents message interception
- **Active Attacks:** Message integrity verification
- **Device Compromise:** Panic mode for immediate data destruction
- **Network Analysis:** No central points of failure

## User Experience Design

### Design Principles
- **Simplicity:** Minimal interface, essential features only
- **Accessibility:** Support for low-literacy users
- **Speed:** Critical actions complete in under 30 seconds
- **Reliability:** Offline-first design with graceful degradation
- **Cultural Sensitivity:** Multilingual support, culturally appropriate design

### User Interface Requirements

#### Main Screen
- **Alert List:** Chronological display of received alerts
- **Create Button:** Prominent, one-tap alert creation
- **Status Indicator:** Bluetooth connectivity and mesh status
- **Settings Access:** Minimal configuration options

#### Alert Creation Screen
- **City Field:** Text input with autocomplete
- **Street Field:** Text input with recent locations
- **Description Field:** Multiline text with character counter
- **Send Button:** Prominent, disabled until valid input
- **Cancel Button:** Return to main screen

#### Settings Screen
- **Expiry Timer:** Configurable message retention
- **Language Selection:** Multilingual support
- **Panic Mode:** Emergency data deletion
- **About:** Version information and help

### Accessibility Features
- **Screen Reader Support:** Full VoiceOver/TalkBack compatibility
- **High Contrast Mode:** Enhanced visibility options
- **Large Text Support:** Scalable font sizes
- **Voice Input:** Speech-to-text for alert creation
- **Haptic Feedback:** Tactile confirmation of actions

### Internationalization
- **Primary Languages:** English, Spanish, Haitian Creole
- **Additional Languages:** Based on community needs
- **Cultural Adaptation:** Appropriate terminology and imagery
- **RTL Support:** Right-to-left language compatibility

## Performance Requirements

### Response Time
- **Alert Creation:** < 2 seconds from tap to broadcast
- **Message Reception:** < 5 seconds from transmission to display
- **Bluetooth Discovery:** < 10 seconds for device connection
- **Panic Mode:** < 3 seconds for complete data deletion

### Scalability
- **Concurrent Users:** Support 50+ devices in mesh network
- **Message Throughput:** 10 messages per minute per device
- **Storage Capacity:** 1000+ cached messages
- **Battery Efficiency:** < 5% battery drain per hour

### Reliability
- **Uptime:** 99.9% availability when Bluetooth enabled
- **Message Delivery:** 95% success rate within range
- **Data Integrity:** Zero message corruption
- **Crash Recovery:** Automatic restart with data preservation

## Quality Assurance

### Testing Strategy

#### Unit Testing
- **Coverage:** 80% minimum code coverage
- **Focus Areas:** Encryption, message validation, data storage
- **Automation:** Continuous integration testing
- **Mocking:** External dependencies mocked

#### Integration Testing
- **Bluetooth Communication:** Device-to-device message transmission
- **Database Operations:** CRUD operations and encryption
- **UI Components:** User interaction flows
- **Security Features:** Encryption and secure deletion

#### User Acceptance Testing
- **Community Testing:** Real-world testing with target users
- **Accessibility Testing:** Screen reader and mobility testing
- **Performance Testing:** Battery usage and response times
- **Security Testing:** Penetration testing and vulnerability assessment

### Quality Metrics
- **Bug Density:** < 1 critical bug per 1000 lines of code
- **Performance:** All operations within specified time limits
- **Security:** Zero high-severity vulnerabilities
- **Accessibility:** WCAG 2.1 AA compliance

## Deployment & Distribution

### Distribution Strategy
- **Primary:** Open source GitHub repository
- **Secondary:** Direct APK distribution for Android
- **Future:** F-Droid repository for alternative distribution

### Release Process
1. **Code Review:** All changes require peer review
2. **Testing:** Automated and manual testing completion
3. **Security Audit:** Independent security review
4. **Community Feedback:** Beta testing with target communities
5. **Documentation:** User guides and technical documentation
6. **Release:** Tagged version with release notes

### Versioning
- **Semantic Versioning:** MAJOR.MINOR.PATCH format
- **Backward Compatibility:** Maintained for protocol versions
- **Migration Support:** Automatic data migration between versions

## Risk Analysis

### Technical Risks
- **Bluetooth Reliability:** Mitigation through robust error handling
- **Platform Fragmentation:** Minimum SDK requirements and testing
- **Battery Drain:** Optimization and user education
- **Message Delivery:** Redundancy and retry mechanisms

### Security Risks
- **Encryption Weakness:** Regular security audits and updates
- **Device Compromise:** Panic mode and secure deletion
- **Network Attacks:** End-to-end encryption and validation
- **Side Channel Attacks:** Timing analysis prevention

### Legal Risks
- **Regulatory Compliance:** Privacy law adherence
- **Content Liability:** User-generated content disclaimers
- **Export Controls:** Encryption export compliance
- **Platform Policies:** App store policy compliance

### Social Risks
- **Misinformation:** Community moderation and verification
- **Misuse:** Clear terms of service and intended use
- **Surveillance:** Privacy-first design and education
- **Community Safety:** Responsible disclosure and support

## Success Metrics

### Technical Metrics
- **Adoption Rate:** Number of active installations
- **Message Volume:** Daily alert transmission count
- **Network Growth:** Mesh network size and connectivity
- **Performance:** Response time and reliability metrics

### Impact Metrics
- **Community Safety:** Reported incidents and response times
- **User Feedback:** Satisfaction and usability scores
- **Security Incidents:** Zero compromises of user data
- **Accessibility:** Usage by target demographic

### Development Metrics
- **Code Quality:** Test coverage and defect density
- **Community Engagement:** Contributor count and activity
- **Documentation:** Completeness and accuracy
- **Support:** Response time to issues and questions

## Future Roadmap

### Phase 1: MVP (Months 1-3)
- Core alert creation and broadcasting
- Basic Bluetooth mesh networking
- Essential security features
- Android application development

### Phase 2: Enhancement (Months 4-6)
- Multi-hop mesh networking
- iOS application development
- Advanced encryption features
- Offline mapping integration

### Phase 3: Expansion (Months 7-12)
- Additional platform support
- Enhanced user interface
- Community management tools
- Integration with external services

### Phase 4: Sustainability (Year 2+)
- Long-term maintenance model
- Community governance structure
- Funding and resource allocation
- Ecosystem development

## Contributing Guidelines

### Code Contribution
- **Fork and Pull Request:** Standard GitHub workflow
- **Code Standards:** Platform-specific style guides
- **Testing Requirements:** Unit tests for all new features
- **Documentation:** Inline comments and README updates

### Non-Code Contribution
- **Design:** UI/UX mockups and user research
- **Translation:** Localization for target languages
- **Testing:** Community testing and feedback
- **Documentation:** User guides and technical documentation

### Community Guidelines
- **Respectful Communication:** Inclusive and supportive environment
- **Security First:** Responsible disclosure of vulnerabilities
- **Privacy Protection:** No sharing of user data or testing information
- **Mission Alignment:** Contributions support project goals

## Conclusion

MeshWatch represents a critical tool for community safety and empowerment, providing secure, decentralized communication capabilities for at-risk populations. Through careful design, robust security, and community-driven development, this project aims to create a sustainable, impactful solution that protects vulnerable communities while respecting their privacy and autonomy.

The success of MeshWatch depends on collaboration between technologists, community organizers, and affected populations. By maintaining a focus on user needs, security, and accessibility, this project can serve as a model for community-driven technology development that prioritizes human rights and social justice.

---

**Document Version:** 1.0  
**Last Updated:** July 11, 2025  
**Next Review:** August 11, 2025