# Component Documentation - Retail-Lite POS

## Table of Contents
1. [Layout Components](#layout-components)
2. [Form Components](#form-components)
3. [Navigation Components](#navigation-components)
4. [Card Components](#card-components)
5. [Button Components](#button-components)
6. [Icon Components](#icon-components)
7. [Responsive Components](#responsive-components)
8. [Animation Components](#animation-components)
9. [Typography System](#typography-system)
10. [Color System](#color-system)

---

## Layout Components

### Container System

#### `.container`
Primary content wrapper with max-width and responsive padding.

```css
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}
```

**Usage:**
```html
<div class="container">
    <!-- Content goes here -->
</div>
```

**Responsive Behavior:**
- Desktop: 1200px max-width with 20px horizontal padding
- Mobile: Full width with maintained padding

### Grid Systems

#### Feature Grid (`.features-grid`)
Responsive grid layout for feature cards with automatic wrapping.

```css
.features-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 2rem;
    padding: 2rem;
}

@media (max-width: 768px) {
    .features-grid {
        flex-direction: column;
        align-items: center;
    }
}
```

**Usage:**
```html
<div class="features-grid">
    <div class="feature-card">...</div>
    <div class="feature-card">...</div>
    <div class="feature-card">...</div>
</div>
```

#### Test Users Grid (`.test-users-grid`)
Grid layout for displaying test user accounts.

```css
.test-users-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
    margin-top: 1rem;
}
```

---

## Form Components

### Input Groups

#### `.input-group`
Styled input wrapper with icon support.

```css
.input-group {
    position: relative;
    margin-bottom: 1rem;
}

.input-group i {
    position: absolute;
    left: 15px;
    top: 50%;
    transform: translateY(-50%);
    color: #666;
}

.input-group input {
    width: 100%;
    padding: 12px 15px 12px 45px;
    border: 2px solid #ddd;
    border-radius: 8px;
    font-size: 1rem;
}
```

**Usage:**
```html
<div class="input-group">
    <i class="fas fa-envelope"></i>
    <input type="text" placeholder="Email or Phone Number" required />
</div>
```

### Form Layouts

#### Login Form (`.login-form`)
Styled container for login forms.

```css
.login-form {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    max-width: 400px;
    margin: 2rem auto;
}
```

#### Signup Card (`.signup-card`)
Enhanced styling for registration forms.

```css
.signup-card {
    background: rgba(255,255,255,0.95);
    backdrop-filter: blur(10px);
    padding: 2.5rem;
    border-radius: 15px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.1);
}
```

---

## Navigation Components

### Header Components

#### Hero Header (`.hero`)
Main header with gradient background and overlay effects.

```css
.hero {
    background: linear-gradient(135deg, #2E7D32 0%, #FF5722 100%);
    color: white;
    padding: 80px 0;
    text-align: center;
    position: relative;
    overflow: hidden;
}

.hero::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: url('data:image/svg+xml;...');
    opacity: 0.2;
}
```

**Usage:**
```html
<header class="hero">
    <div class="container">
        <div class="logo">...</div>
        <div class="tagline">...</div>
    </div>
</header>
```

#### Language Switcher (`.language-switcher`)
Positioned language selection component.

```css
.language-switcher {
    position: absolute;
    top: 20px;
    right: 20px;
    z-index: 100;
}
```

### Logo Component

#### `.logo`
Brand identity component with icon and text.

```css
.logo {
    font-size: 1.4rem;
    margin-bottom: 20px;
    font-weight: 600;
}

.logo i {
    margin-right: 8px;
    color: var(--secondary);
}
```

**Usage:**
```html
<div class="logo">
    <i class="fas fa-cash-register"></i> 
    <strong>Retail-Lite POS</strong>
</div>
```

---

## Card Components

### Feature Cards

#### `.feature-card`
Individual feature showcase card with icon, title, and description.

```css
.feature-card {
    background: white;
    padding: 2rem;
    border-radius: 15px;
    text-align: center;
    box-shadow: 0 5px 15px rgba(0,0,0,0.08);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    max-width: 350px;
}

.feature-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 30px rgba(0,0,0,0.15);
}
```

#### `.feature-icon`
Icon container within feature cards.

```css
.feature-icon {
    width: 80px;
    height: 80px;
    margin: 0 auto 1.5rem;
    background: linear-gradient(45deg, var(--primary), var(--accent));
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    color: white;
}
```

**Usage:**
```html
<div class="feature-card">
    <div class="feature-icon">
        <i class="fas fa-bolt"></i>
    </div>
    <h3>Super Fast</h3>
    <p>Process sales in seconds, even with slow internet.</p>
</div>
```

### Dashboard Cards

#### `.cards` & `.card`
Dashboard navigation cards for different modules.

```css
.cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
    margin: 2rem 0;
}

.card {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    text-align: center;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    cursor: pointer;
    transition: all 0.3s ease;
}

.card:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 20px rgba(0,0,0,0.15);
}

.card i {
    font-size: 2.5rem;
    color: var(--primary);
    margin-bottom: 1rem;
}
```

**Usage:**
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
</div>
```

---

## Button Components

### Primary Buttons

#### `.btn-primary`
Main call-to-action button with gradient background.

```css
.btn-primary {
    background: linear-gradient(45deg, #2E7D32, #4CAF50);
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 50px;
    font-size: 1.1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(46, 125, 50, 0.3);
}
```

#### `.btn-secondary`
Secondary action button with outline style.

```css
.btn-secondary {
    background: transparent;
    color: white;
    border: 2px solid white;
    padding: 12px 25px;
    border-radius: 50px;
    text-decoration: none;
    font-weight: 500;
    transition: all 0.3s ease;
}

.btn-secondary:hover {
    background: white;
    color: var(--primary);
}
```

### Floating Action Buttons

#### Chat Button (`#open-chatbot`)
Fixed positioned chat interface trigger.

```css
#open-chatbot {
    position: fixed;
    bottom: 90px;
    right: 20px;
    background: #2E7D32;
    color: white;
    border: none;
    border-radius: 50%;
    width: 56px;
    height: 56px;
    font-size: 1.5rem;
    cursor: pointer;
    box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    z-index: 10000;
    transition: all 0.3s ease;
}

#open-chatbot:hover {
    transform: scale(1.1);
    box-shadow: 0 6px 15px rgba(0,0,0,0.3);
}
```

### Social Contact Buttons

#### WhatsApp Button
```css
.whatsapp-btn {
    position: fixed;
    bottom: 150px;
    right: 20px;
    background: #25D366;
    color: white;
    border-radius: 50%;
    width: 56px;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.8rem;
    text-decoration: none;
    box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    z-index: 10000;
}
```

#### Email Button
```css
.email-btn {
    position: fixed;
    bottom: 210px;
    right: 20px;
    background: #D44638;
    color: white;
    border-radius: 50%;
    width: 56px;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.4rem;
    text-decoration: none;
    box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    z-index: 10000;
}
```

---

## Icon Components

### Feature Icons

Icon classes used throughout the application with semantic meaning:

#### Business Operations
- `.fas fa-cash-register` - Sales/POS operations
- `.fas fa-box` - Inventory management
- `.fas fa-chart-bar` - Reports and analytics
- `.fas fa-money-bill-wave` - Payment processing

#### Technology Features
- `.fas fa-bolt` - Speed/Performance
- `.fas fa-mobile-alt` - Mobile compatibility
- `.fas fa-wifi-slash` - Offline capabilities
- `.fas fa-chart-line` - Growth/Analytics

#### User Interface
- `.fas fa-building` - Business information
- `.fas fa-envelope` - Contact/Email
- `.fas fa-lock` - Security/Password
- `.fas fa-handshake` - Welcome/Greeting

#### Social Media
- `.fab fa-whatsapp` - WhatsApp contact
- `.fas fa-map-marker-alt` - Location

**Usage Example:**
```html
<div class="feature-icon">
    <i class="fas fa-bolt"></i>
</div>
```

---

## Responsive Components

### Mobile Adaptations

#### Mobile Hero
```css
@media (max-width: 768px) {
    .hero {
        padding: 60px 0;
    }
    
    .tagline h1 {
        font-size: 2.2rem;
    }
    
    .signup-card, .login-form {
        margin: 20px 15px;
        padding: 20px;
    }
}
```

#### Mobile Feature Grid
```css
@media (max-width: 768px) {
    .feature-grid {
        flex-direction: column;
        align-items: center;
    }
    
    .feature {
        max-width: 90%;
    }
}
```

#### Mobile Cards
```css
@media (max-width: 768px) {
    .cards {
        grid-template-columns: 1fr;
        gap: 1rem;
    }
    
    .card {
        padding: 1.5rem;
    }
}
```

---

## Animation Components

### Hover Effects

#### Card Hover Animation
```css
.feature-card,
.card {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.feature-card:hover,
.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 30px rgba(0,0,0,0.15);
}
```

#### Button Hover Animation
```css
.btn-primary,
.btn-secondary {
    transition: all 0.3s ease;
}

.btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(46, 125, 50, 0.3);
}
```

### Background Animations

#### Hero Overlay Animation
```css
.hero::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" preserveAspectRatio="none"><path d="M0,0 L100,0 L100,100 Z" fill="rgba(255,255,255,0.1)"/></svg>');
    opacity: 0.2;
}
```

---

## Typography System

### Font Families
```css
body {
    font-family: 'Poppins', sans-serif;
}

/* Alternative font stack */
.alternative {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
```

### Heading Hierarchy
```css
h1 {
    font-size: 2.5rem;
    font-weight: 700;
    line-height: 1.2;
}

h2 {
    font-size: 2rem;
    font-weight: 600;
    margin-bottom: 1rem;
}

h3 {
    font-size: 1.5rem;
    font-weight: 500;
    margin-bottom: 0.75rem;
}
```

### Text Styles
```css
.tagline {
    font-size: 1.2rem;
    opacity: 0.9;
    line-height: 1.6;
}

.small {
    font-size: 0.9rem;
    color: #666;
}

.stats {
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}
```

---

## Color System

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
    
    /* Alternative color scheme */
    --alt-primary: #FF5722;
    --alt-dark: #2E7D32;
    --alt-light: #f9f9f9;
    --alt-text: #333;
}
```

### Color Usage Guidelines

#### Primary Colors
- `--primary` (#000000): Main brand color, primary buttons
- `--secondary` (#FFD700): Accent elements, highlights
- `--accent` (#E67E22): Call-to-action elements

#### Semantic Colors
- `--success` (#28A745): Success states, positive actions
- `--dark` (#333333): Text, headers
- `--light` (#F5F5F5): Backgrounds, cards

#### Gradient Combinations
```css
/* Hero gradient */
background: linear-gradient(135deg, #2E7D32 0%, #FF5722 100%);

/* Button gradient */
background: linear-gradient(45deg, #2E7D32, #4CAF50);

/* Icon gradient */
background: linear-gradient(45deg, var(--primary), var(--accent));
```

---

## Implementation Examples

### Complete Feature Card Implementation
```html
<div class="features-grid">
    <div class="feature-card">
        <div class="feature-icon">
            <i class="fas fa-bolt"></i>
        </div>
        <h3>Super Fast</h3>
        <p>Process sales in seconds, even with slow internet. Our offline mode keeps you selling anytime!</p>
    </div>
    <div class="feature-card">
        <div class="feature-icon">
            <i class="fas fa-mobile-alt"></i>
        </div>
        <h3>Mobile Friendly</h3>
        <p>Manage your business from anywhere using your phone, tablet, or computer.</p>
    </div>
</div>
```

### Complete Form Implementation
```html
<div class="login-form">
    <h2>Retailer Login</h2>
    <form id="loginForm">
        <div class="input-group">
            <i class="fas fa-envelope"></i>
            <input type="text" id="contact" placeholder="Email or Phone Number" required />
        </div>
        <div class="input-group">
            <i class="fas fa-lock"></i>
            <input type="password" id="password" placeholder="Password" required />
        </div>
        <button type="submit" class="btn-primary">Login</button>
    </form>
</div>
```

---

*This component documentation provides detailed styling and usage information for all UI components in the Retail-Lite POS system. Use these components consistently throughout the application for a cohesive user experience.*