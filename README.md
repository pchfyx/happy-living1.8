# Happy Living - Kost Management System

A complete cloud-based boarding house (kost) management system built with Firebase.

## 🚀 Features

### Authentication & Security
- User registration with email verification
- Secure login system
- Email verification required before access
- Automatic verification email sending (Webmailer)

### CRUD Operations (12 Total)
**Rooms Management:**
- ✅ Create new room
- ✅ Read/View all rooms
- ✅ Update room details
- ✅ Delete room

**Tenants Management:**
- ✅ Create new tenant
- ✅ Read/View all tenants
- ✅ Update tenant information
- ✅ Delete tenant

**Payments Management:**
- ✅ Create payment record
- ✅ Read/View all payments
- ✅ Update payment status
- ✅ Delete payment

**Maintenance Management:**
- ✅ Create maintenance request
- ✅ Read/View all requests
- ✅ Update request status
- ✅ Delete request

## 📁 Project Structure

```
happyliving-kost/
├── index.html              # Main HTML file
├── css/
│   └── style.css          # All styling
└── js/
    ├── firebase-config.js  # Firebase configuration
    ├── auth.js            # Authentication module
    ├── rooms.js           # Rooms CRUD
    ├── tenants.js         # Tenants CRUD
    ├── payments.js        # Payments CRUD
    ├── maintenance.js     # Maintenance CRUD
    └── main.js            # Main UI controller
```

## 🔧 Setup Instructions

### 1. Firebase Configuration
Your Firebase is already configured in `js/firebase-config.js`:
- Project: happyliving-2872b
- Database: Asia Southeast (Singapore)
- Authentication enabled
- Realtime Database enabled

### 2. Enable Firebase Services

#### Enable Authentication:
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project: `happyliving-2872b`
3. Go to **Authentication** → **Sign-in method**
4. Enable **Email/Password** provider
5. Click **Save**

#### Enable Email Verification:
1. In Authentication settings, go to **Templates**
2. Customize the **Email address verification** template (optional)
3. The system will automatically send verification emails

#### Enable Realtime Database:
1. Go to **Realtime Database** in Firebase Console
2. If not created, click **Create Database**
3. Choose **Asia Southeast (Singapore)** region
4. Start in **Test mode** (for development)
5. Update security rules:

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    },
    "rooms": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "tenants": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "payments": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "maintenance": {
      ".read": "auth != null",
      ".write": "auth != null"
    }
  }
}
```

### 3. Deploy the Application

#### Option A: Local Testing
1. Install a local web server (required for ES6 modules):
   ```bash
   # Using Python
   python -m http.server 8000
   
   # Using Node.js http-server
   npx http-server
   ```

2. Open browser: `http://localhost:8000`

#### Option B: Firebase Hosting
1. Install Firebase CLI:
   ```bash
   npm install -g firebase-tools
   ```

2. Login to Firebase:
   ```bash
   firebase login
   ```

3. Initialize hosting:
   ```bash
   firebase init hosting
   ```
   - Select your project: `happyliving-2872b`
   - Set public directory: `.` (current directory)
   - Configure as single-page app: `No`
   - Don't overwrite index.html

4. Deploy:
   ```bash
   firebase deploy
   ```

#### Option C: Other Hosting Services
- **Netlify**: Drag and drop your folder
- **Vercel**: Connect your GitHub repo
- **GitHub Pages**: Push to gh-pages branch

## 📖 How to Use

### First Time Setup
1. **Register an account:**
   - Enter your full name, email, phone, and password
   - Click "Register"
   - Check your email inbox for verification link
   - Click the verification link in email

2. **Login:**
   - Use your registered email and password
   - You must verify your email first before logging in

### Managing Rooms
1. Click **"Add New Room"** button
2. Enter room details:
   - Room Number (e.g., "101", "A-12")
   - Room Type (Single/Double/Shared)
   - Monthly Price (in Rupiah)
   - Status (Available/Occupied/Maintenance)
3. Click **"Save Room"**
4. To edit or delete, use buttons on room cards

### Managing Tenants
1. Click **"Add New Tenant"** button
2. Enter tenant information:
   - Full Name
   - Email address
   - Phone number
   - ID Card number (KTP)
   - Move-in date
3. Click **"Save Tenant"**
4. Edit or delete using card buttons

### Managing Payments
1. Click **"Add Payment"** button
2. Enter payment details:
   - Tenant name
   - Room number
   - Amount (Rupiah)
   - Payment date
   - Status (Paid/Pending/Overdue)
3. Click **"Save Payment"**
4. Track all payment records

### Managing Maintenance
1. Click **"Add Request"** button
2. Enter maintenance details:
   - Room number
   - Issue description
   - Priority (Low/Medium/High)
   - Status (Pending/In Progress/Completed)
3. Click **"Save Request"**
4. Update status as work progresses

## 🔒 Security Features

- Email verification required for all new users
- Authentication required for database access
- Secure password requirements (minimum 6 characters)
- Real-time data synchronization
- User-specific data access control

## 💡 Tips

1. **Test Email Verification**: Use a real email address for testing
2. **Check Spam Folder**: Verification emails might go to spam
3. **Firebase Quotas**: Free tier has daily limits
4. **Backup Data**: Export your database regularly
5. **Production Rules**: Update database rules for production

## 🐛 Troubleshooting

### "Email not verified" error
- Check your email inbox and spam folder
- Click the verification link in the email
- Try logging in again after verification

### Cannot access database
- Ensure you're logged in
- Check Firebase Console for database rules
- Verify your internet connection

### Module not found errors
- Must use a web server (not file:// protocol)
- Use Python, Node.js, or hosting service

### Email not received
- Check spam/junk folder
- Wait a few minutes (can take up to 10 minutes)
- Try registering with a different email
- Check Firebase Console → Authentication → Templates

## 📊 Database Structure

```
firebase-database/
├── users/
│   └── {userId}/
│       ├── name
│       ├── email
│       ├── phone
│       └── emailVerified
├── rooms/
│   └── {roomId}/
│       ├── roomNumber
│       ├── type
│       ├── price
│       └── status
├── tenants/
│   └── {tenantId}/
│       ├── name
│       ├── email
│       ├── phone
│       ├── idCard
│       └── moveInDate
├── payments/
│   └── {paymentId}/
│       ├── tenant
│       ├── room
│       ├── amount
│       ├── date
│       └── status
└── maintenance/
    └── {maintenanceId}/
        ├── room
        ├── issue
        ├── priority
        └── status
```

## 🎨 Customization

### Change Colors
Edit `css/style.css`:
```css
/* Primary color */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Button colors */
background: #667eea;
```

### Add More Fields
1. Update HTML form in `index.html`
2. Modify corresponding CRUD file in `js/`
3. Update database write/read operations

## 📝 License

This project is open source and available for educational purposes.

## 🤝 Support

For issues or questions:
1. Check Firebase Console for errors
2. Review browser console for JavaScript errors
3. Verify all Firebase services are enabled
4. Check database security rules

## 🎯 Future Enhancements

- [ ] Dashboard with statistics
- [ ] Payment reminders via email
- [ ] Invoice generation (PDF)
- [ ] Tenant portal
- [ ] Multiple property support
- [ ] Financial reports
- [ ] Image upload for rooms
- [ ] Contract management

---

**Built with ❤️ using Firebase**