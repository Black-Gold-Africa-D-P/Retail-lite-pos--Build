# JavaScript API Reference - Retail-Lite POS

## Table of Contents
1. [Core APIs](#core-apis)
2. [Authentication APIs](#authentication-apis)
3. [Storage APIs](#storage-apis)
4. [Event Management](#event-management)
5. [Navigation APIs](#navigation-apis)
6. [DOM Manipulation](#dom-manipulation)
7. [Utility Functions](#utility-functions)
8. [Error Handling](#error-handling)
9. [Configuration](#configuration)
10. [Integration Examples](#integration-examples)

---

## Core APIs

### Application Initialization

#### `DOMContentLoaded` Event Handler
**Purpose**: Initializes the application when the DOM is fully loaded.

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const user = JSON.parse(localStorage.getItem('retailLiteUser'));
    if (!user) {
        window.location.href = 'index.html';
        return;
    }
    document.getElementById('userName').textContent = user.businessName || 'Retailer';
});
```

**Parameters**: None  
**Returns**: Void  
**Side Effects**: 
- Checks authentication status
- Redirects unauthenticated users
- Updates UI with user information

#### Test Users Initialization
**Purpose**: Sets up default test users for development and demo purposes.

```javascript
const testUsers = [
    { businessName: "Alpha Retail", contact: "alpha@example.com", password: "alpha123" },
    { businessName: "Beta Traders", contact: "beta@example.com", password: "beta123" }
];

if (!localStorage.getItem('retailLiteTestUsers')) {
    localStorage.setItem('retailLiteTestUsers', JSON.stringify(testUsers));
}
```

**Parameters**: None  
**Returns**: Void  
**Side Effects**: Populates localStorage with test user data

---

## Authentication APIs

### Login System

#### `loginForm` Event Handler
**Purpose**: Handles user authentication through form submission.

```javascript
document.getElementById('loginForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const contactInput = document.getElementById('contact').value.trim().toLowerCase();
    const passwordInput = document.getElementById('password').value.trim();
    
    const users = JSON.parse(localStorage.getItem('retailLiteTestUsers') || '[]');
    const user = users.find(u => 
        u.contact.toLowerCase() === contactInput && 
        u.password === passwordInput
    );
    
    if (user) {
        localStorage.setItem('retailLiteUser', JSON.stringify({ 
            businessName: user.businessName, 
            contact: user.contact 
        }));
        window.location.href = 'dashboard.html';
    } else {
        alert('Invalid contact or password.');
    }
});
```

**Parameters**:
- `e` (Event): Form submission event

**Returns**: Void

**Side Effects**:
- Validates user credentials
- Creates user session
- Redirects to dashboard on success
- Shows error message on failure

**Form Elements Required**:
- `#contact` (input): Email or phone number field
- `#password` (input): Password field

#### Authentication Validation
**Purpose**: Validates user credentials against stored data.

```javascript
function validateCredentials(contact, password) {
    const users = JSON.parse(localStorage.getItem('retailLiteTestUsers') || '[]');
    return users.find(u => 
        u.contact.toLowerCase() === contact.toLowerCase() && 
        u.password === password
    );
}
```

**Parameters**:
- `contact` (string): User's contact information
- `password` (string): User's password

**Returns**: User object if valid, undefined if invalid

### Logout System

#### `logout` Function
**Purpose**: Logs out the current user and redirects to landing page.

```javascript
function logout() {
    localStorage.removeItem('retailLiteUser');
    window.location.href = 'index.html';
}
```

**Parameters**: None  
**Returns**: Void  
**Side Effects**: 
- Clears user session
- Redirects to login page

#### Logout Button Handler
**Purpose**: Handles logout button click events.

```javascript
document.getElementById('logoutBtn').addEventListener('click', () => {
    localStorage.removeItem('retailLiteUser');
    window.location.href = 'index.html';
});
```

**Parameters**: None  
**Returns**: Void  
**Required Elements**: `#logoutBtn` button element

---

## Storage APIs

### User Session Management

#### `setUserSession(userData)`
**Purpose**: Stores user session data in localStorage.

```javascript
function setUserSession(userData) {
    const sessionData = {
        businessName: userData.businessName,
        contact: userData.contact,
        loginTime: new Date().toISOString()
    };
    localStorage.setItem('retailLiteUser', JSON.stringify(sessionData));
}
```

**Parameters**:
- `userData` (object): User information to store

**Returns**: Void  
**Side Effects**: Updates localStorage with session data

#### `getUserSession()`
**Purpose**: Retrieves current user session data.

```javascript
function getUserSession() {
    try {
        return JSON.parse(localStorage.getItem('retailLiteUser'));
    } catch (error) {
        console.error('Error parsing user session:', error);
        return null;
    }
}
```

**Parameters**: None  
**Returns**: User session object or null  
**Error Handling**: Returns null if parsing fails

#### `clearUserSession()`
**Purpose**: Removes user session data from localStorage.

```javascript
function clearUserSession() {
    localStorage.removeItem('retailLiteUser');
}
```

**Parameters**: None  
**Returns**: Void  
**Side Effects**: Removes session data from localStorage

### Test Users Management

#### `getTestUsers()`
**Purpose**: Retrieves test users from localStorage.

```javascript
function getTestUsers() {
    return JSON.parse(localStorage.getItem('retailLiteTestUsers') || '[]');
}
```

**Parameters**: None  
**Returns**: Array of test user objects

#### `initializeTestUsers()`
**Purpose**: Sets up default test users if none exist.

```javascript
function initializeTestUsers() {
    if (!localStorage.getItem('retailLiteTestUsers')) {
        const defaultUsers = [
            { businessName: "Alpha Retail", contact: "alpha@example.com", password: "alpha123" },
            { businessName: "Beta Traders", contact: "beta@example.com", password: "beta123" }
        ];
        localStorage.setItem('retailLiteTestUsers', JSON.stringify(defaultUsers));
    }
}
```

**Parameters**: None  
**Returns**: Void  
**Side Effects**: Populates localStorage with test users

---

## Event Management

### Form Event Handlers

#### Generic Form Submission Handler
**Purpose**: Template for handling form submissions with validation.

```javascript
function handleFormSubmission(formId, validationFn, successFn, errorFn) {
    document.getElementById(formId).addEventListener('submit', function(e) {
        e.preventDefault();
        
        const formData = new FormData(this);
        const data = Object.fromEntries(formData);
        
        if (validationFn && !validationFn(data)) {
            if (errorFn) errorFn('Validation failed');
            return;
        }
        
        if (successFn) successFn(data);
    });
}
```

**Parameters**:
- `formId` (string): ID of the form element
- `validationFn` (function): Function to validate form data
- `successFn` (function): Function to call on successful validation
- `errorFn` (function): Function to call on error

**Returns**: Void

#### Click Event Management
**Purpose**: Centralized click event handling.

```javascript
function addClickHandler(elementId, handler) {
    const element = document.getElementById(elementId);
    if (element) {
        element.addEventListener('click', handler);
    } else {
        console.warn(`Element with ID '${elementId}' not found`);
    }
}
```

**Parameters**:
- `elementId` (string): ID of the element
- `handler` (function): Click event handler function

**Returns**: Void

---

## Navigation APIs

### Page Navigation

#### `navigateTo(page)`
**Purpose**: Programmatic navigation between pages.

```javascript
function navigateTo(page) {
    window.location.href = page;
}
```

**Parameters**:
- `page` (string): Target page URL

**Returns**: Void  
**Side Effects**: Changes browser location

#### `redirectToDashboard()`
**Purpose**: Redirects authenticated users to dashboard.

```javascript
function redirectToDashboard() {
    const user = getUserSession();
    if (user) {
        window.location.href = 'dashboard.html';
    }
}
```

**Parameters**: None  
**Returns**: Void  
**Preconditions**: User must be authenticated

#### `redirectToLogin()`
**Purpose**: Redirects unauthenticated users to login page.

```javascript
function redirectToLogin() {
    window.location.href = 'index.html';
}
```

**Parameters**: None  
**Returns**: Void

### Route Protection

#### `requireAuthentication()`
**Purpose**: Ensures user is authenticated before accessing protected pages.

```javascript
function requireAuthentication() {
    const user = getUserSession();
    if (!user) {
        redirectToLogin();
        return false;
    }
    return true;
}
```

**Parameters**: None  
**Returns**: Boolean indicating authentication status  
**Side Effects**: Redirects to login if not authenticated

---

## DOM Manipulation

### Element Updates

#### `updateUserName(userName)`
**Purpose**: Updates the displayed user name in the UI.

```javascript
function updateUserName(userName) {
    const userNameElement = document.getElementById('userName');
    if (userNameElement) {
        userNameElement.textContent = userName || 'Retailer';
    }
}
```

**Parameters**:
- `userName` (string): Name to display

**Returns**: Void  
**Required Elements**: `#userName` element

#### `updateElementText(elementId, text)`
**Purpose**: Generic function to update element text content.

```javascript
function updateElementText(elementId, text) {
    const element = document.getElementById(elementId);
    if (element) {
        element.textContent = text;
    } else {
        console.warn(`Element with ID '${elementId}' not found`);
    }
}
```

**Parameters**:
- `elementId` (string): ID of the target element
- `text` (string): Text content to set

**Returns**: Void

### Form Manipulation

#### `clearForm(formId)`
**Purpose**: Clears all input fields in a form.

```javascript
function clearForm(formId) {
    const form = document.getElementById(formId);
    if (form) {
        form.reset();
    }
}
```

**Parameters**:
- `formId` (string): ID of the form to clear

**Returns**: Void

#### `getFormData(formId)`
**Purpose**: Extracts data from a form as an object.

```javascript
function getFormData(formId) {
    const form = document.getElementById(formId);
    if (!form) return {};
    
    const formData = new FormData(form);
    return Object.fromEntries(formData);
}
```

**Parameters**:
- `formId` (string): ID of the form

**Returns**: Object containing form field values

---

## Utility Functions

### Input Validation

#### `validateEmail(email)`
**Purpose**: Validates email address format.

```javascript
function validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}
```

**Parameters**:
- `email` (string): Email address to validate

**Returns**: Boolean indicating validity

#### `validatePhone(phone)`
**Purpose**: Validates phone number format (Kenyan format).

```javascript
function validatePhone(phone) {
    const phoneRegex = /^(\+254|0)[7-9]\d{8}$/;
    return phoneRegex.test(phone.replace(/\s/g, ''));
}
```

**Parameters**:
- `phone` (string): Phone number to validate

**Returns**: Boolean indicating validity

#### `validatePassword(password)`
**Purpose**: Validates password strength.

```javascript
function validatePassword(password) {
    return password && password.length >= 6;
}
```

**Parameters**:
- `password` (string): Password to validate

**Returns**: Boolean indicating validity

### String Utilities

#### `sanitizeInput(input)`
**Purpose**: Sanitizes user input to prevent XSS.

```javascript
function sanitizeInput(input) {
    const div = document.createElement('div');
    div.textContent = input;
    return div.innerHTML;
}
```

**Parameters**:
- `input` (string): Input string to sanitize

**Returns**: Sanitized string

#### `formatBusinessName(name)`
**Purpose**: Formats business name for display.

```javascript
function formatBusinessName(name) {
    return name.trim().replace(/\s+/g, ' ');
}
```

**Parameters**:
- `name` (string): Business name to format

**Returns**: Formatted business name

---

## Error Handling

### Error Display

#### `showError(message, elementId)`
**Purpose**: Displays error messages to users.

```javascript
function showError(message, elementId = null) {
    if (elementId) {
        const element = document.getElementById(elementId);
        if (element) {
            element.textContent = message;
            element.className = 'error-message';
        }
    } else {
        alert(message);
    }
}
```

**Parameters**:
- `message` (string): Error message to display
- `elementId` (string, optional): ID of element to show error in

**Returns**: Void

#### `clearErrors(elementId)`
**Purpose**: Clears error messages from the UI.

```javascript
function clearErrors(elementId) {
    const element = document.getElementById(elementId);
    if (element) {
        element.textContent = '';
        element.className = '';
    }
}
```

**Parameters**:
- `elementId` (string): ID of element to clear

**Returns**: Void

### Error Logging

#### `logError(error, context)`
**Purpose**: Logs errors for debugging purposes.

```javascript
function logError(error, context = '') {
    console.error(`[Retail-Lite POS] ${context}:`, error);
}
```

**Parameters**:
- `error` (Error|string): Error to log
- `context` (string): Context information

**Returns**: Void

---

## Configuration

### Application Settings

#### Default Configuration
```javascript
const APP_CONFIG = {
    APP_NAME: 'Retail-Lite POS',
    VERSION: '1.0.0',
    STORAGE_PREFIX: 'retailLite',
    DEFAULT_PAGE: 'index.html',
    DASHBOARD_PAGE: 'dashboard.html',
    SESSION_TIMEOUT: 24 * 60 * 60 * 1000, // 24 hours
    MAX_LOGIN_ATTEMPTS: 3
};
```

#### Feature Flags
```javascript
const FEATURES = {
    OFFLINE_MODE: true,
    MPESA_INTEGRATION: true,
    MULTI_LANGUAGE: false,
    ADVANCED_REPORTING: true
};
```

### API Endpoints (Future Implementation)
```javascript
const API_CONFIG = {
    BASE_URL: 'https://api.retail-lite.co.ke',
    ENDPOINTS: {
        LOGIN: '/auth/login',
        LOGOUT: '/auth/logout',
        DASHBOARD: '/dashboard',
        SALES: '/sales',
        INVENTORY: '/inventory',
        REPORTS: '/reports'
    }
};
```

---

## Integration Examples

### Complete Authentication Flow
```javascript
// Initialize application
document.addEventListener('DOMContentLoaded', () => {
    initializeTestUsers();
    
    if (window.location.pathname.includes('dashboard.html')) {
        if (!requireAuthentication()) return;
        
        const user = getUserSession();
        updateUserName(user.businessName);
        setupDashboard();
    }
});

// Setup login form
function setupLoginForm() {
    handleFormSubmission('loginForm', 
        validateLoginData, 
        handleLoginSuccess, 
        handleLoginError
    );
}

function validateLoginData(data) {
    return data.contact && data.password;
}

function handleLoginSuccess(data) {
    const user = validateCredentials(data.contact, data.password);
    if (user) {
        setUserSession(user);
        redirectToDashboard();
    } else {
        showError('Invalid credentials');
    }
}

function handleLoginError(message) {
    showError(message, 'login-error');
}
```

### Dashboard Initialization
```javascript
function setupDashboard() {
    addClickHandler('logoutBtn', () => {
        clearUserSession();
        redirectToLogin();
    });
    
    // Setup dashboard cards
    setupDashboardCards();
    
    // Initialize modules
    initializeSalesModule();
    initializeInventoryModule();
    initializeReportsModule();
}

function setupDashboardCards() {
    const cardActions = {
        'new-sale': () => navigateToSales(),
        'inventory': () => navigateToInventory(),
        'reports': () => navigateToReports(),
        'mpesa-sync': () => initializeMpesaSync()
    };
    
    Object.keys(cardActions).forEach(cardId => {
        addClickHandler(cardId, cardActions[cardId]);
    });
}
```

### Error Handling Integration
```javascript
// Global error handler
window.addEventListener('error', (e) => {
    logError(e.error, 'Global Error');
    showError('An unexpected error occurred. Please try again.');
});

// Promise rejection handler
window.addEventListener('unhandledrejection', (e) => {
    logError(e.reason, 'Unhandled Promise Rejection');
    e.preventDefault();
});
```

---

## API Usage Patterns

### Chaining Operations
```javascript
// Method chaining for user operations
class UserManager {
    setUser(userData) {
        setUserSession(userData);
        return this;
    }
    
    updateDisplay() {
        const user = getUserSession();
        updateUserName(user?.businessName);
        return this;
    }
    
    redirect() {
        redirectToDashboard();
        return this;
    }
}

// Usage
new UserManager()
    .setUser(userData)
    .updateDisplay()
    .redirect();
```

### Event-driven Architecture
```javascript
// Custom event system for module communication
const EventBus = {
    events: {},
    
    on(event, callback) {
        if (!this.events[event]) {
            this.events[event] = [];
        }
        this.events[event].push(callback);
    },
    
    emit(event, data) {
        if (this.events[event]) {
            this.events[event].forEach(callback => callback(data));
        }
    }
};

// Usage
EventBus.on('user:login', (user) => {
    updateUserName(user.businessName);
    redirectToDashboard();
});

EventBus.emit('user:login', userData);
```

---

*This JavaScript API reference provides comprehensive documentation for all programming interfaces in the Retail-Lite POS system. Use these APIs consistently to maintain code quality and system reliability.*