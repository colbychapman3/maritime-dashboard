# Maritime Operations Dashboard

A comprehensive multi-ship operations management system with real-time tracking, team coordination, and analytics.

## 🚢 Features

- **Master Dashboard**: Overview of all active ship operations with real-time statistics
- **Ship Details**: Comprehensive view of individual ship operations with progress tracking
- **Team Management**: Auto and heavy operations team coordination
- **Real-time Updates**: Live progress tracking and status updates
- **Analytics**: Performance metrics and operational insights
- **Calendar View**: Schedule and timeline management
- **Responsive Design**: Modern UI that works on all devices

## 🔧 Recent Fix: Navigation Bug Resolution

### Issue
Previously, selecting an active ship from the master dashboard incorrectly redirected users to the create wizard instead of showing ship details.

### Solution
- **Created dedicated ship details page** (`static/ship-details.html`)
- **Added new Flask route** (`/ship-details`) in `src/main.py`
- **Fixed navigation function** in `static/master-dashboard.html`:
  - Changed `viewShipDetails()` from `/?ship=${shipId}` to `/ship-details?id=${shipId}`
- **Enhanced user experience** with comprehensive ship information display

### Navigation Flow (Fixed)
```
Master Dashboard → Select Ship → Ship Details Page ✅
(Previously: Master Dashboard → Select Ship → Create Wizard ❌)
```

## 🚀 Setup Instructions

### Prerequisites
- Python 3.8+
- Flask
- Flask-CORS

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/colbychapman3/maritime-dashboard.git
   cd maritime-dashboard
   ```

2. **Install dependencies**
   ```bash
   pip install flask flask-cors
   ```

3. **Run the application**
   ```bash
   python src/main.py
   ```

4. **Access the application**
   - Master Dashboard: `http://localhost:5000/master`
   - Ship Details: `http://localhost:5000/ship-details?id={ship_id}`
   - Create Wizard: `http://localhost:5000/`
   - Analytics: `http://localhost:5000/analytics`
   - Calendar: `http://localhost:5000/calendar`

## 📁 Project Structure

```
maritime-dashboard/
├── src/
│   ├── main.py              # Flask application with routes
│   ├── models/              # Database models
│   └── routes/              # API endpoints
│       ├── ships.py         # Ship operations API
│       ├── user.py          # User management
│       └── file_processor.py
├── static/
│   ├── master-dashboard.html # Main operations dashboard
│   ├── ship-details.html    # Individual ship details page
│   ├── index.html           # Create wizard
│   ├── analytics.html       # Analytics dashboard
│   └── calendar.html        # Calendar view
└── database/
    └── ships.json           # Ship data storage
```

## 🔗 API Endpoints

### Ships Management
- `GET /api/ships` - Get all ships
- `GET /api/ships/{id}` - Get specific ship details
- `POST /api/ships` - Create new ship operation
- `PUT /api/ships/{id}` - Update ship operation
- `PUT /api/ships/{id}/progress` - Update ship progress
- `PUT /api/ships/{id}/status` - Update ship status
- `DELETE /api/ships/{id}` - Delete ship operation

### Additional Endpoints
- `GET /api/ships/berths` - Get berth occupancy status
- `GET /api/ships/stats` - Get operations statistics
- `GET /api/analytics` - Get analytics data

## 🎯 Ship Details Page Features

The new ship details page includes:

- **Vessel Information**: Name, type, port, berth, company, operation type
- **Operation Details**: Date, shift times, vehicle counts
- **Progress Tracking**: Interactive circular progress indicator with update controls
- **Team Information**: Auto and heavy operations team assignments
- **Targets & Performance**: BRV, ZEE, SOU targets and expected rates
- **Quick Actions**: Status update buttons (Active, Loading, Discharge, Paused, Complete)
- **Navigation**: Back button and dashboard link
- **Error Handling**: Proper error states for non-existent ships

## 🔄 Testing the Fix

1. **Start the application**
2. **Create a test ship** (if none exist):
   ```bash
   curl -X POST http://localhost:5000/api/ships \
     -H "Content-Type: application/json" \
     -d '{"vesselName": "Test Vessel", "vesselType": "Container Ship", "port": "Test Port", "operationDate": "2025-07-04", "company": "Test Company", "operationType": "Discharge", "berthLocation": "Berth 1"}'
   ```
3. **Navigate to master dashboard**: `http://localhost:5000/master`
4. **Click on a ship card** - Should now redirect to ship details page
5. **Verify URL**: Should be `/ship-details?id={ship_id}` not `/?ship={ship_id}`

## 🛠️ Technologies Used

- **Backend**: Python Flask
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Styling**: Tailwind CSS
- **Icons**: Font Awesome
- **Charts**: Chart.js
- **Data Storage**: JSON files (SQLite ready)

## 📝 License

This project is licensed under the MIT License.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

---

**Navigation Bug Status**: ✅ **RESOLVED** - Ship selection now correctly redirects to ship details page instead of create wizard.