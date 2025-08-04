# Ruckit-Geotab Integration Suite

A comprehensive fleet management integration solution that provides seamless synchronization between Geotab and Ruckit platforms. This suite consists of a Python backend service for real-time location synchronization and two Geotab add-ins for credential management and asset overview.

## 🚀 Overview

The Ruckit-Geotab Integration Suite solves the critical problem of maintaining accurate, synchronized location data across multiple fleet management platforms. By automatically detecting and correcting location discrepancies, this integration ensures that your fleet data remains consistent and reliable across both Geotab and Ruckit systems.

## 📦 Suite Components

### 1. Backend Synchronization Service
**Repository**: [`ruckit-integration-backend`](https://github.com/parkerhendry/ruckit-integration-backend)

A Python-based service that continuously monitors and synchronizes location data between Geotab and Ruckit APIs.

**Key Features:**
- Real-time location discrepancy detection (2-minute polling cycles)
- Automatic coordinate correction and synchronization
- Configurable tolerance levels for coordinate matching
- Comprehensive error handling and retry logic
- Detailed logging and monitoring capabilities

### 2. Device Mapping Button Add-In
**Repository**: [`ruckit-integration-frontend-dropdown`](https://github.com/parkerhendry/ruckit-integration-frontend-dropdown)

A Geotab custom button add-in that provides an intuitive dropdown interface for managing Ruckit API credentials and device mappings directly from device pages.

**Key Features:**
- Context-aware device mapping interface
- Real-time credential validation and conflict detection
- Elegant dropdown UI with company branding
- Create, update, and clear mapping operations
- Keyboard shortcuts and accessibility support

### 3. Assets Overview Add-In
**Repository**: [`ruckit-integration-frontend-menu`](https://github.com/parkerhendry/ruckit-integration-frontend-menu)

A Geotab page add-in that displays all Ruckit device mappings in a searchable, organized table format for fleet management oversight.

**Key Features:**
- Comprehensive asset overview with search functionality
- Real-time filtering and navigation capabilities
- Direct links to Geotab device pages
- Responsive design for desktop and mobile
- Automatic refresh and data synchronization

---

## 🔗 Repository Links

| Component | Repository | Description |
|-----------|------------|-------------|
| Backend Service | [`ruckit-integration-backend`](https://github.com/parkerhendry/ruckit-integration-backend) | Python synchronization service |
| Button Add-In | [`ruckit-integration-frontend-dropdown`](https://github.com/parkerhendry/ruckit-integration-frontend-dropdown) | Device mapping interface |
| Assets List Add-In | [`ruckit-integration-frontend-menu`](https://github.com/parkerhendry/ruckit-integration-frontend-menu) | Asset overview dashboard |

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    Geotab MyGeotab Platform                     │
├─────────────────────┬───────────────────┬─────────────────────┤
│   Button Add-In     │   Assets Add-In   │    AddInData API    │
│                     │                   │                     │
│ • Device Mapping    │ • Asset Overview  │ • Credential Store  │
│ • Credential Entry  │ • Search & Filter │ • Device Mappings   │
│ • Validation        │ • Navigation      │ • Configuration     │
└─────────────────────┴───────────────────┴─────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                  Python Backend Service                        │
│                                                                 │
│ • Reads mappings from Geotab AddInData                        │
│ • Polls location data from both APIs                          │
│ • Detects coordinate discrepancies                            │
│ • Synchronizes locations automatically                        │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                        Ruckit API                              │
│                                                                 │
│ • Receives location updates                                    │
│ • Maintains synchronized coordinates                           │
│ • Provides driver and device data                             │
└─────────────────────────────────────────────────────────────────┘
```

## 🔄 Data Flow

1. **Configuration Setup**
   - Fleet managers use the Button Add-In to configure Ruckit API credentials for each device
   - Credentials are stored securely in Geotab's AddInData system
   - Assets Add-In provides oversight of all configured mappings

2. **Automatic Synchronization**
   - Backend service retrieves configuration data from Geotab
   - Service polls location data from both Geotab and Ruckit APIs
   - Coordinate discrepancies are detected using configurable tolerance levels
   - Corrections are automatically pushed to Ruckit when mismatches are found

3. **Monitoring and Management**
   - Comprehensive logging tracks all synchronization activities
   - Assets Add-In provides real-time visibility into mapping status
   - Button Add-In allows immediate updates to credentials and mappings

## 🛠️ Installation & Setup

### Prerequisites
- Python 3.7+ for backend service
- Geotab MyGeotab database with administrator privileges
- Ruckit API access and credentials
- Network connectivity between all systems

### Quick Start

1. **Clone the Parent Repository**
   ```bash
   git clone https://github.com/parkerhendry/ruckit-integration
   cd ruckit-geotab-integration-suite
   ```

2. **Initialize Submodules**
   ```bash
   git submodule init
   git submodule update
   ```

3. **Install Backend Service**
   ```bash
   cd ruckit-integration-backend
   pip install -r requirements.txt
   cp .env.example .env
   # Configure your Geotab credentials in .env
   ```

4. **Install Geotab Add-Ins**
   - Navigate to MyGeotab → Administration → System → Add-Ins
   - Install the Button Add-In from `ruckit-integration-frontend-dropdown/` directory
   - Install the Assets Add-In from `ruckit-integration-frontend-menu/` directory
   - Configure company branding and settings as needed

5. **Start the System**
   ```bash
   # Start backend service
   cd ruckit-integration-backend
   python ruckit.py
   
   # Add-ins are now available in MyGeotab interface
   ```

## ⚙️ Configuration

### Environment Variables
Create a `.env` file in the backend service directory:
```env
GEOTAB_USERNAME=your_geotab_username
GEOTAB_DATABASE=your_geotab_database
GEOTAB_PASSWORD=your_geotab_password
```

### Company Branding
Update logos and styling in both add-ins:
- Button Add-In: Modify logo URL in `addin.js`
- Assets Add-In: Update logo in `ruckitAssets.html`

### Synchronization Settings
Adjust tolerance levels and polling intervals in the backend service configuration.

## 📊 Monitoring & Operations

### Logging
The backend service provides comprehensive logging:
- Authentication status and API connectivity
- Location comparison results and discrepancy detection
- Synchronization success/failure status
- Error conditions and retry attempts

### Health Checks
Monitor system health through:
- Backend service console output
- Assets Add-In for mapping status overview
- Geotab AddInData records for configuration integrity

### Performance Metrics
- **Polling Interval**: 2-minute cycles for near real-time sync
- **Scalability**: Handles hundreds of devices per sync cycle
- **API Efficiency**: Optimized bulk operations to minimize API calls
- **Memory Usage**: Lightweight operation with minimal resource requirements

## 🔒 Security & Compliance

### Data Protection
- API credentials encrypted and stored in Geotab's secure AddInData system
- No sensitive data logged or cached locally
- Proper authentication headers for all API communications
- Network security through HTTPS/TLS connections

### Access Control
- Respects existing Geotab user permissions and roles
- Add-ins inherit MyGeotab security model
- Backend service uses dedicated service credentials

### Audit Trail
- Complete logging of all synchronization activities
- Timestamp tracking for all mapping changes
- Error logging for compliance and debugging