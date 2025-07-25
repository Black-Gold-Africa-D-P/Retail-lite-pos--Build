# Retail-Lite POS API Documentation

## Table of Contents
1. [Overview](#overview)
2. [Authentication System](#authentication-system)
3. [User Management APIs](#user-management-apis)
4. [Frontend Components](#frontend-components)
5. [Navigation System](#navigation-system)
6. [Local Storage APIs](#local-storage-apis)
7. [UI Components](#ui-components)
8. [Event Handlers](#event-handlers)
9. [Usage Examples](#usage-examples)
10. [Component Reference](#component-reference)

## Overview

Retail-Lite POS is a comprehensive Point of Sale system designed for African retailers, SMEs, and enterprises. The system provides both online and offline functionality with M-Pesa integration, inventory management, and smart reporting capabilities.

### System Architecture
- **Frontend**: HTML5, CSS3, JavaScript (Vanilla)
- **Storage**: Local Storage for offline functionality
- **Design**: Responsive, mobile-first approach
- **Authentication**: Client-side user session management

---

## Authentication System

### Login API

**Function**: `document.getElementById('loginForm').addEventListener('submit', function(e))`

Handles user authentication and session management.

#### Parameters
- `contact` (string): User's email or phone number
- `password` (string): User's password

#### Usage Example
```javascript
// Login form HTML structure
<form id="loginForm">
  <input type="text" id="contact" placeholder="Email or Phone Number" required />
  <input type="password" id="password" placeholder="Password" required />
  <button type="submit">Login</button>
</form>

// JavaScript handler (automatically attached)
document.getElementById('loginForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const contactInput = document.getElementById('contact').value.trim().toLowerCase();
    const passwordInput = document.getElementById('password').value.trim();
    
    const users = JSON.parse(localStorage.getItem('retailLiteTestUsers') || '[]');
    const user = users.find(u => u.contact.toLowerCase() === contactInput && u.password === passwordInput);
    
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

#### Test Users
```javascript
const testUsers = [
    { businessName: "Alpha Retail", contact: "alpha@example.com", password: "alpha123" },
    { businessName: "Beta Traders", contact: "beta@example.com", password: "beta123" }
];
```

### Logout API

**Function**: `logout()`

Logs out the current user and redirects to the landing page.

#### Usage Example
```javascript
// Inline onclick handler
<button onclick="logout()">Logout</button>

// Event listener approach
document.getElementById('logoutBtn').addEventListener('click', () => {
    localStorage.removeItem('retailLiteUser');
    window.location.href = 'index.html';
});
```

### Session Management API

**Function**: `DOMContentLoaded` Event Handler

Checks user authentication status and manages session state.

#### Usage Example
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

---

## User Management APIs

### User Registration System

**Form ID**: `signupForm`

Handles new user registration (frontend form structure).

#### HTML Structure
```html
<form id="signupForm">
    <div class="input-group">
        <i class="fas fa-building"></i>
        <input type="text" id="businessName" placeholder="Business Name" required />
    </div>
    <div class="input-group">
        <i class="fas fa-envelope"></i>
        <input type="text" id="contact" placeholder="Email or Phone Number" required />
    </div>
    <div class="input-group">
        <i class="fas fa-lock"></i>
        <input type="password" id="signupPassword" placeholder="Create Password" required />
    </div>
    <button type="submit" class="btn-primary">
        Start Selling Smarter <i class="fas fa-arrow-right"></i>
    </button>
</form>
```

#### Required Fields
- `businessName` (string): Name of the business
- `contact` (string): Email or phone number
- `signupPassword` (string): Password for the account

---

## Frontend Components

### Navigation Components

#### Header Component
**CSS Class**: `.hero`

Main header with branding and call-to-action elements.

```html
<header class="hero">
    <div class="container">
        <div class="logo">
            <i class="fas fa-cash-register"></i> <strong>Retail-Lite POS</strong>
        </div>
        <div class="tagline">
            <h1>Power Your Biashara. <span>Online or Offline.</span></h1>
            <p>Africa's smartest POS for retailers, SMEs, Enterprises</p>
        </div>
    </div>
</header>
```

#### Language Switcher
**CSS Class**: `.language-switcher`

Positioned language selection component.

```css
.language-switcher {
    position: absolute;
    top: 20px;
    right: 20px;
}
```

### Feature Cards

#### Feature Grid Component
**CSS Class**: `.features-grid`

Responsive grid layout for feature cards.

```html
<div class="features-grid">
    <div class="feature-card">
        <div class="feature-icon">
            <i class="fas fa-bolt"></i>
        </div>
        <h3>Super Fast</h3>
        <p>Process sales in seconds, even with slow internet.</p>
    </div>
</div>
```

#### Available Feature Types
1. **Speed Features** - `.fas fa-bolt`
2. **Mobile Features** - `.fas fa-mobile-alt`
3. **Analytics Features** - `.fas fa-chart-line`
4. **Offline Features** - `.fas fa-wifi-slash`
5. **Payment Features** - `.fas fa-money-bill-wave`

---

## Navigation System

### Page Navigation API

#### Dashboard Navigation
```javascript
// Redirect to dashboard after successful login
if (user) {
    localStorage.setItem('retailLiteUser', JSON.stringify(user));
    window.location.href = 'dashboard.html';
}
```

#### Landing Page Navigation
```javascript
// Redirect to landing page after logout
localStorage.removeItem('retailLiteUser');
window.location.href = 'index.html';
```

### Anchor Navigation

#### Section Links
```html
<!-- Navigation to pricing section -->
<a href="#pricing" class="btn btn-primary">Try Free Now!</a>

<!-- Navigation to demo section -->
<a href="#demo" class="btn btn-secondary">Watch Demo</a>

<!-- Navigation to contact section -->
<a href="#contact" class="btn">Get Early Access</a>
```

---

## Local Storage APIs

### User Session Storage

#### Store User Session
```javascript
localStorage.setItem('retailLiteUser', JSON.stringify({
    businessName: user.businessName,
    contact: user.contact
}));
```

#### Retrieve User Session
```javascript
const user = JSON.parse(localStorage.getItem('retailLiteUser'));
```

#### Clear User Session
```javascript
localStorage.removeItem('retailLiteUser');
```

### Test Users Storage

#### Initialize Test Users
```javascript
if (!localStorage.getItem('retailLiteTestUsers')) {
    localStorage.setItem('retailLiteTestUsers', JSON.stringify(testUsers));
}
```

#### Retrieve Test Users
```javascript
const users = JSON.parse(localStorage.getItem('retailLiteTestUsers') || '[]');
```

---

## UI Components

### Button Components

#### Primary Button
```html
<button class="btn-primary">
    Start Selling Smarter <i class="fas fa-arrow-right"></i>
</button>
```

#### Secondary Button
```html
<a href="#demo" class="btn btn-secondary">Watch Demo</a>
```

#### Logout Button
```html
<button id="logoutBtn" style="background:#2E7D32; color:white; border:none; padding:10px 20px; border-radius:8px; cursor:pointer;">
    ← Logout
</button>
```

### Card Components

#### Dashboard Cards
```html
<div class="cards">
    <div class="card">
        <i class="fas fa-cash-register"></i>
        <h3>New Sale</h3>
    </div>
    <div class="card">
        <i class="fas fa-box"></i>
        <h3>Inventory</h3>
    </div>
    <div class="card">
        <i class="fas fa-chart-bar"></i>
        <h3>Reports</h3>
    </div>
    <div class="card">
        <i class="fas fa-money-bill-wave"></i>
        <h3>M-Pesa Sync</h3>
    </div>
</div>
```

### Floating Action Buttons

#### Chat Button
```html
<button id="open-chatbot" style="position: fixed; bottom: 90px; right: 20px; background: #2E7D32; color: white; border: none; border-radius: 50%; width: 56px; height: 56px; font-size: 1.5rem; cursor: pointer; box-shadow: 0 4px 10px rgba(0,0,0,0.2); z-index: 10000;">
    💬
</button>
```

#### WhatsApp Contact Button
```html
<a href="https://wa.me/254710450454" target="_blank" rel="noopener" style="position: fixed; bottom: 150px; right: 20px; background: #25D366; color: white; border-radius: 50%; width: 56px; height: 56px; display: flex; align-items: center; justify-content: center; font-size: 1.8rem; text-decoration: none; box-shadow: 0 4px 10px rgba(0,0,0,0.2); z-index: 10000;">
    <i class="fab fa-whatsapp"></i>
</a>
```

#### Email Contact Button
```html
<a href="mailto:support@retail-lite.co.ke" style="position: fixed; bottom: 210px; right: 20px; background: #D44638; color: white; border-radius: 50%; width: 56px; height: 56px; display: flex; align-items: center; justify-content: center; font-size: 1.4rem; text-decoration: none; box-shadow: 0 4px 10px rgba(0,0,0,0.2); z-index: 10000;">
    ✉️
</a>
```

---

## Event Handlers

### Form Submission Handlers

#### Login Form Handler
```javascript
document.getElementById('loginForm').addEventListener('submit', function(e) {
    e.preventDefault();
    // Authentication logic
});
```

#### DOM Ready Handler
```javascript
document.addEventListener('DOMContentLoaded', () => {
    // Session management logic
});
```

#### Click Event Handlers
```javascript
document.getElementById('logoutBtn').addEventListener('click', () => {
    // Logout logic
});
```

---

## Usage Examples

### Complete Authentication Flow

```javascript
// 1. User submits login form
document.getElementById('loginForm').addEventListener('submit', function(e) {
    e.preventDefault();
    
    // 2. Validate credentials
    const contactInput = document.getElementById('contact').value.trim().toLowerCase();
    const passwordInput = document.getElementById('password').value.trim();
    
    // 3. Check against stored users
    const users = JSON.parse(localStorage.getItem('retailLiteTestUsers') || '[]');
    const user = users.find(u => 
        u.contact.toLowerCase() === contactInput && 
        u.password === passwordInput
    );
    
    // 4. Handle authentication result
    if (user) {
        // Store session
        localStorage.setItem('retailLiteUser', JSON.stringify({
            businessName: user.businessName,
            contact: user.contact
        }));
        
        // Redirect to dashboard
        window.location.href = 'dashboard.html';
    } else {
        alert('Invalid contact or password.');
    }
});
```

### Session Management Example

```javascript
// Check authentication on page load
document.addEventListener('DOMContentLoaded', () => {
    const user = JSON.parse(localStorage.getItem('retailLiteUser'));
    
    if (!user) {
        // Not authenticated, redirect to login
        window.location.href = 'index.html';
        return;
    }
    
    // Update UI with user information
    document.getElementById('userName').textContent = 
        user.businessName || 'Retailer';
    
    // Setup logout functionality
    document.getElementById('logoutBtn').addEventListener('click', () => {
        localStorage.removeItem('retailLiteUser');
        window.location.href = 'index.html';
    });
});
```

---

## Component Reference

### CSS Custom Properties

```css
:root {
    --primary: #000000;
    --secondary: #FFD700;
    --accent: #E67E22;
    --light: #F5F5F5;
    --dark: #333333;
    --earth: #8B4513;
    --success: #28A745;
}
```

### Responsive Breakpoints

```css
@media (max-width: 768px) {
    .features-grid {
        flex-direction: column;
        align-items: center;
    }
    
    .feature {
        max-width: 90%;
    }
}
```

### Animation Classes

```css
.hero::before {
    content: '';
    position: absolute;
    background: url('data:image/svg+xml;...');
    opacity: 0.2;
}
```

---

## Contact and Support

### Contact Information
- **Email**: support@retail-lite.co.ke
- **WhatsApp**: +254710450454
- **Company**: Black Gold Digital Platforms
- **Location**: Nairobi, Kenya

### External Resources
- **Font Awesome**: https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css
- **Google Fonts**: https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap

---

## File Structure

```
/
├── index.html              # Main landing page with login/signup
├── dashboard.html          # Dashboard page (post-authentication)
├── Tuma-Biasahara-yako-ju.html  # Alternative landing page
├── README.md              # Basic project information
├── LICENSE                # License file
├── hero-1.png            # Hero background image
├── Dashboard Retaillite.png  # Dashboard screenshot
├── Retail-lite Pos Logo.png  # Logo image
└── web adds (1-6).png    # Marketing/promotional images
```

---

*This documentation covers all public APIs, functions, and components in the Retail-Lite POS system. For additional features or custom implementations, refer to the source code or contact the development team.*