# Employee Attendance System

A comprehensive attendance tracking system built with React, TypeScript, Supabase, and Tailwind CSS. Features separate dashboards for employees and managers with real-time attendance tracking, reporting, and analytics.

## Features

### Employee Features
- **Authentication**: Secure login and registration
- **Dashboard**: View daily attendance status and monthly statistics
- **Check In/Out**: Mark attendance with automatic late detection (after 9:15 AM)
- **Attendance History**: Calendar view with color-coded attendance status
- **Monthly Summary**: Track present, absent, late days, and total hours
- **Profile Management**: Update personal information

### Manager Features
- **Dashboard**: Overview of team attendance with statistics
- **Team Attendance**: View all employees' attendance records with filtering
- **Reports**: Generate and export attendance reports to CSV
- **Weekly Trends**: Visualize attendance patterns
- **Absent Employees**: Quick view of who's absent today

## Tech Stack

- **Frontend**: React 18 + TypeScript
- **Styling**: Tailwind CSS
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth
- **Build Tool**: Vite
- **Icons**: Lucide React

## Database Schema

### Users Table
- `id` (UUID) - Primary key, references auth.users
- `name` (TEXT) - User's full name
- `email` (TEXT) - User's email (unique)
- `role` (TEXT) - 'employee' or 'manager'
- `employee_id` (TEXT) - Unique identifier (e.g., EMP001)
- `department` (TEXT) - User's department
- `created_at` (TIMESTAMP) - Account creation timestamp

### Attendance Table
- `id` (UUID) - Primary key
- `user_id` (UUID) - References users table
- `date` (DATE) - Attendance date
- `check_in_time` (TIMESTAMP) - Check-in timestamp
- `check_out_time` (TIMESTAMP) - Check-out timestamp
- `status` (TEXT) - 'present', 'absent', 'late', or 'half-day'
- `total_hours` (DECIMAL) - Total hours worked
- `created_at` (TIMESTAMP) - Record creation timestamp

## Setup Instructions

### Prerequisites
- Node.js 18+ installed
- npm or yarn package manager
- A Supabase account (free tier works)

### 1. Clone the Repository
```bash
git clone https://github.com/arikuttibhaskarmanasa/attendancesystem.git
cd employee-attendance-system
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Environment Variables
The `.env` file is already configured with Supabase credentials:
```
VITE_SUPABASE_URL=your-supabase-url
VITE_SUPABASE_ANON_KEY=your-supabase-anon-key
```

### 4. Database Setup
The database schema has been automatically created with Row Level Security (RLS) policies:
- Users can view and update their own data
- Managers can view all users' data
- Users can manage their own attendance records
- Managers can view all attendance records

### 5. Run the Application
```bash
npm run dev
```

The application will open at `http://localhost:5173`

### 6. Build for Production
```bash
npm run build
```

## Usage Guide

### For Employees

1. **Register**: Create an account with your details
   - Provide: Name, Email, Employee ID, Department
   - Choose role: Employee

2. **Check In**: Click "Check In" on the dashboard
   - Automatic status: Present (before 9:15 AM) or Late (after 9:15 AM)

3. **Check Out**: Click "Check Out" when leaving
   - System automatically calculates hours worked

4. **View History**: Navigate to "Attendance History"
   - Calendar view with color-coded days
   - Click any day to see detailed information

### For Managers

1. **Register**: Create an account with Manager role

2. **Dashboard**: View team statistics
   - Total employees
   - Present/Absent/Late count for today
   - Weekly attendance trends
   - List of absent employees

3. **All Attendance**: View and filter all records
   - Filter by employee, status, or date
   - Search by name or employee ID

4. **Reports**: Generate attendance reports
   - Select date range
   - Filter by specific employee or all
   - Export to CSV format

## Sample Users

You can create test accounts with the following examples:

**Employee Account**
- Name: John Doe
- Email: john@example.com
- Employee ID: EMP001
- Department: Engineering
- Role: Employee

**Manager Account**
- Name: Jane Smith
- Email: jane@example.com
- Employee ID: MGR001
- Department: Management
- Role: Manager

## Color Coding

- 🟢 **Green**: Present
- 🔴 **Red**: Absent
- 🟡 **Yellow**: Late
- 🟠 **Orange**: Half Day

## Key Features Explained

### Automatic Late Detection
- Check-in after 9:15 AM automatically marks status as "Late"
- Check-in before 9:15 AM marks status as "Present"

### Hours Calculation
- Automatically calculated when checking out
- Based on difference between check-in and check-out times

### Row Level Security
- Database-level security ensures users only access their own data
- Managers have elevated permissions to view team data
- All queries are secured at the database level

### CSV Export
- Export attendance reports with all relevant fields
- Includes employee details, timestamps, and status
- Compatible with Excel and other spreadsheet applications

## Project Structure

```
src/
├── components/
│   └── Layout.tsx              # Main layout with navigation
├── contexts/
│   └── AuthContext.tsx         # Authentication context
├── lib/
│   └── supabase.ts             # Supabase client configuration
├── pages/
│   ├── employee/
│   │   ├── EmployeeDashboard.tsx
│   │   └── AttendanceHistory.tsx
│   ├── manager/
│   │   ├── ManagerDashboard.tsx
│   │   ├── AllEmployeesAttendance.tsx
│   │   └── Reports.tsx
│   ├── Login.tsx
│   ├── Register.tsx
│   └── Profile.tsx
├── App.tsx                     # Main application component
└── main.tsx                    # Application entry point
```

## Security Features

- Password-based authentication via Supabase
- Row Level Security (RLS) on all tables
- Secure API calls with authentication tokens
- Role-based access control
- No sensitive data exposed in client code

## Performance Optimizations

- Efficient database queries with proper indexing
- Lazy loading of attendance data
- Optimized re-renders with React best practices
- Minimal bundle size with Vite

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

MIT License

## Support

For issues or questions, please open an issue on the GitHub repository.
