# HR Management System

A **web-based Human Resource Management System (HRMS)** designed to help organizations efficiently manage employee data, leaves, and salary details, with role-based access for HR and employees.

![Node.js](https://img.shields.io/badge/Node.js-backend-green) ![React](https://img.shields.io/badge/React-frontend-blue) ![MySQL](https://img.shields.io/badge/MySQL-database-orange)


---

## 🌟 Features

- **Employee Management:** Add, edit, view, and delete employee details  
- **Leave Management:** Apply, approve, reject, and filter leaves by date  
- **Salary Management:** Record, edit, and delete salary information with date tracking  
- **Role-Based Access:** Different dashboards and permissions for HR and employees  
- **Search & Filters:** Quickly search employees, leave applications, and salary records  
- **Responsive UI:** Works on desktop and mobile devices  

---

## 🏗️ Architecture

**User (Browser)** → **Frontend (React)** → **Backend API (Node.js/Express)** → **Database (MySQL)** → **Data Display / Reports**

### Flow

1. **Login & Role Detection:** Users log in as HR or Employee  
2. **Employee Dashboard:** View and manage employee records  
3. **Leave Management:** Employees apply for leaves; HR can approve/reject  
4. **Salary Management:** HR manages salary records; employees can view  
5. **Reports & Filtering:** Generate lists and apply filters for analysis  

---

## 🛠️ Tech Stack

### Frontend
- React.js  
- CSS for styling  

### Backend
- Node.js (Express.js)  
- MySQL database  
- RESTful APIs for CRUD operations  

> **Note:** The system stores employee, leave, and salary data securely in MySQL. Session management ensures role-based access control.

---

## 🚀 Setup & Installation

### Environment Setup

1. Clone the repository:
```bash
git clone https://github.com/D1YaRaJ/HR_Management_System.git
cd HR_Management_System
```

2. **Install backend dependencies**
```bash
cd backend
npm install
```

3. **Install frontend dependencies**
```bash
cd ../frontend
npm install
```

4. **Configure environment variables**

   **Backend (.env)**
   ```env
   DB_HOST=localhost
   DB_USER=your_username
   DB_PASSWORD=your_password
   DB_NAME=hr_management
   JWT_SECRET=your_jwt_secret
   PORT=5000
   ```

   **Frontend (.env)**
   ```env
   REACT_APP_API_URL=http://localhost:5000
   ```

5. **Database Setup**
```bash
# Create MySQL database
mysql -u root -p -e "CREATE DATABASE hr_management;"

# Import database schema (if provided)
mysql -u username -p hr_management < database/schema.sql
```

6. **Run the backend server**
```bash
cd backend
npm start
```

7. **Run the frontend development server**
```bash
cd frontend
npm start
```

8. **Access the application**
Open your browser and navigate to:
```
http://localhost:3000
```

---

## 📱 Usage Guide

### For Administrators/HR
1. **Dashboard Overview**: View system statistics and recent activities
2. **Employee Management**: Add, edit, or deactivate employee records
3. **Leave Management**: Approve or reject employee leave applications
4. **Payroll Processing**: Manage salary records and payments
5. **Department Management**: Create and manage organizational departments

### For Employees
1. **Profile Management**: View personal information
2. **Leave Applications**: Submit and track leave requests
3. **Salary View**: Access salary history and payslips
4. **Dashboard**: View personal statistics

---

## 📋 API Endpoints Reference

| Endpoint | Method | Description | Authentication |
|----------|--------|-------------|----------------|
| `/login` | POST | HR user authentication | Public |
| `/faculty-login` | POST | Employee/faculty authentication | Public |
| `/faculty-update-password` | POST | Employee password update | Employee |
| `/generate-eid` | GET | Generate next available employee ID | HR/Admin |
| `/add-employee` | POST | Add new employee to system | HR/Admin |
| `/employee/:eid` | GET | Get specific employee details | HR/Admin/Employee |
| `/employee/:eid` | PUT | Update employee information | HR/Admin |
| `/employee/:eid` | DELETE | Delete employee record | HR/Admin |
| `/employees/full` | GET | Get all employees with full details | HR/Admin |
| `/view-employees` | GET | View employees with search functionality | HR/Admin |
| `/generate-did` | GET | Generate next available department ID | HR/Admin |
| `/add-department` | POST | Add new department | HR/Admin |
| `/view-departments` | GET | View departments with search | HR/Admin |
| `/department/:did` | PUT | Update department information | HR/Admin |
| `/department/:did` | DELETE | Delete department | HR/Admin |
| `/apply-leave` | POST | Apply for leave | Employee |
| `/api/colleagues/:eid` | GET | Get list of colleagues for handover | Employee |
| `/assign-leave` | POST | Assign leave quotas to employees | HR/Admin |
| `/get-employees` | GET | Get employee list for leave assignment | HR/Admin |
| `/get-leave-data` | GET | Get leave data for specific year | HR/Admin |
| `/view-leave` | GET | View leave requests | HR/Admin/Employee |
| `/update-leave-status/:id` | PUT | Update leave request status | HR/Admin |
| `/add-salary` | POST | Add salary record for employee | HR/Admin |
| `/update-salary/:eid` | PUT | Update employee salary | HR/Admin |
| `/view-salary` | GET | View all salary records | HR/Admin |
| `/delete-salary/:eid` | DELETE | Delete salary record | HR/Admin |
| `/api/faculty/salary/:eid` | GET | Get salary details for faculty | Employee |
| `/api/salary/update` | POST | Update salary with history tracking | HR/Admin |
| `/api/payroll/:eid/:year/:month` | GET | Get payroll data for specific period | HR/Admin/Employee |
| `/api/payroll/download/:eid/:year/:month` | GET | Download payslip as PDF | HR/Admin/Employee |

---

## 🔐 Authentication & Authorization

### User Types
1. **HR/Admin**: Full system access
2. **Employee/Faculty**: Limited access to personal data

### Authentication Flow
- Login endpoints return success status
- Session management through backend
- Role-based access control for all endpoints

---

## 💰 Salary Calculation Logic

The system automatically calculates:
- **PF (Provident Fund)**: 12% of basic salary
- **TDS (Tax Deducted at Source)**: Progressive tax calculation based on annual income
- **Net Salary**: Total salary minus deductions

### TDS Calculation Table
| Annual Income | Tax Rate |
|---------------|----------|
| Up to ₹3,00,000 | 0% |
| ₹3,00,001 - ₹7,00,000 | 5% |
| ₹7,00,001 - ₹10,00,000 | 10% |
| ₹10,00,001 - ₹12,00,000 | 15% |
| ₹12,00,001 - ₹15,00,000 | 20% |
| Above ₹15,00,000 | 30% |

---

## 🧪 Testing

### Running Tests
```bash
# Run backend tests
cd backend
npm test

# Run frontend tests
cd frontend
npm test
```

### Test Categories
- **API Tests**: Endpoint validation and response testing
- **Component Tests**: React component functionality
- **Integration Tests**: Frontend-Backend integration
- **Security Tests**: Authentication and authorization validation

---

## 🔒 Security Features

- **JWT Authentication**: Secure token-based authentication
- **Password Hashing**: bcrypt for secure password storage
- **Role-Based Access Control**: Different permissions for Admin, HR, and Employees
- **SQL Injection Prevention**: Parameterized queries
- **CORS Configuration**: Controlled cross-origin requests
- **Input Validation**: Server-side validation of all inputs

---

## 🚀 Deployment

### Production Deployment Steps

1. **Build the frontend**
```bash
cd frontend
npm run build
```

2. **Set production environment variables**
```env
NODE_ENV=production
DB_HOST=production-db-host
DB_USER=production-user
DB_PASSWORD=production-password
JWT_SECRET=strong-production-secret
```

3. **Deploy backend to production server**
```bash
# Using PM2 for process management
pm2 start backend/server.js --name hr-backend
```

4. **Serve frontend build**
```bash
# Using Nginx to serve static files
server {
    listen 80;
    server_name your-domain.com;
    
    location / {
        root /path/to/frontend/build;
        index index.html;
        try_files $uri $uri/ /index.html;
    }
    
    location /api {
        proxy_pass http://localhost:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

5. **Database backup setup**
```bash
# Configure regular database backups
mysqldump -u username -p hr_management > backup_$(date +%Y%m%d).sql
```

---


<div align="center">

### 💼 Streamlining HR Processes for Modern Organizations

**Built with React.js, Node.js, and MySQL**

</div>



