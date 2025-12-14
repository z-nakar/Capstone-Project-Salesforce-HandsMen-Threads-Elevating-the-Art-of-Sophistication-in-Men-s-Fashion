# HandsMen Threads: Elevating the Art of Sophistication in Men's Fashion

## Capstone Project Documentation

**Project Title:** HandsMen Threads - Men's Fashion E-Commerce Platform  
**Platform:** Salesforce  
**Date:** November 2025  
**Student:** M.J. Tuplano

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Project Overview](#project-overview)
3. [System Architecture](#system-architecture)
4. [Core Features](#core-features)
5. [Custom Objects](#custom-objects)
6. [Automation & Business Logic](#automation--business-logic)
7. [Email Notifications](#email-notifications)
8. [Technical Implementation](#technical-implementation)
9. [User Interface](#user-interface)
10. [Testing & Validation](#testing--validation)
11. [Future Enhancements](#future-enhancements)
12. [Conclusion](#conclusion)

---

## Executive Summary

HandsMen Threads is a sophisticated men's fashion e-commerce platform built on Salesforce. The system streamlines the entire order management process, from customer account creation to inventory management, automated order calculations, and customer communications. This capstone project demonstrates the integration of custom Salesforce objects, automation flows, Apex triggers, batch jobs, and email templates to create a complete business solution.

---

## Project Overview

### Project Objectives

- Create a fully functional e-commerce platform for men's fashion products
- Implement automated inventory management with low stock alerts
- Develop comprehensive order processing with automated calculations
- Establish customer loyalty program with automated communications
- Ensure data validation and error handling throughout the application

### Key Technologies

- **Platform:** Salesforce Lightning
- **Programming:** Apex (Triggers, Batch Jobs, Handlers)
- **Automation:** Salesforce Flow
- **Communication:** Email Templates & Alerts
- **Data Model:** Custom Salesforce Objects

---

## System Architecture

The HandsMen Threads application is built on a custom Salesforce architecture consisting of:

1. **Custom Objects Layer** - Core data entities (Customers, Products, Inventory, Orders)
2. **Business Logic Layer** - Apex Triggers and Handlers for calculations and validations
3. **Automation Layer** - Salesforce Flows for workflow automation
4. **Integration Layer** - Email templates and notification systems
5. **Batch Processing Layer** - Scheduled jobs for inventory monitoring

### Data Flow Diagram

```
Customer Creation → Product Management → Inventory Tracking → Order Processing → Email Notifications
                                              ↓
                                    Batch Job Monitoring
                                              ↓
                                    Low Stock Alerts
```

---

## Core Features

### 1. Customer Management
- Custom customer account creation interface
- Email validation and error handling
- Customer profile management

![Create Account](SCREENSHOTS/Create%20Account.png)

![Email Validation Error](SCREENSHOTS/Email%20Validation%20Error.png)

### 2. Product Catalog
- Comprehensive product creation system
- Product details and specifications
- Product categorization

![Product Creation](SCREENSHOTS/Handsmen%20Thread%20Product%20Creation.png)

### 3. Inventory Management
- Real-time inventory tracking
- Stock level monitoring
- Automated low stock alerts
- Batch job for scheduled inventory checks

![Inventory Creation](SCREENSHOTS/Handsmen%20Thread%20Inventory%20Creation.png)

![Inventory Batch Job](SCREENSHOTS/InventoryBatchJob.png)

### 4. Order Processing
- Streamlined order creation interface
- Automated order total calculations
- Stock deduction upon order placement
- Order confirmation system

![Order Creation](SCREENSHOTS/Handsmen%20Thread%20Order%20Creation.png)

![Order Calculation Trigger](SCREENSHOTS/Order%20Calculation%20Trigger.png)

![Stock Deduction Trigger](SCREENSHOTS/Stock%20Deduction%20Trigger.png)

### 5. Customer Communications
- Order confirmation emails
- Low stock alert notifications
- Loyalty program communications

![Order Confirmation Email](SCREENSHOTS/Order%20Confirmation%20Email.png)

![Low Stock Alert Email](SCREENSHOTS/Low%20Stock%20Alert%20Email.png)

---

## Custom Objects

### Customer Object
**Purpose:** Store and manage customer information

**Key Fields:**
- Customer Name
- Email Address
- Contact Information
- Account Status
- Loyalty Program Enrollment

**Validations:**
- Email format validation
- Duplicate email prevention
- Required field enforcement

![Customer Creation Form](SCREENSHOTS/Handsmen%20Thread%20Customer%20Creation.png)

---

### Product Object
**Purpose:** Manage product catalog and specifications

**Key Fields:**
- Product Name
- Product Description
- Product Category
- Price
- SKU/Product Code

![Product Object Form](SCREENSHOTS/Handsmen%20Thread%20Product%20Creation.png)

---

### Inventory Object
**Purpose:** Track stock levels and inventory status

**Key Fields:**
- Product Reference (Lookup)
- Current Stock Quantity
- Reorder Level
- Last Updated Date
- Stock Status

**Business Rules:**
- Triggers low stock alerts when quantity falls below threshold
- Updates automatically when orders are placed
- Monitored by batch job for proactive alerts

![Inventory Object Form](SCREENSHOTS/Handsmen%20Thread%20Inventory%20Creation.png)

---

### Order Object
**Purpose:** Manage customer orders and transactions

**Key Fields:**
- Customer Reference (Lookup)
- Product Reference (Lookup)
- Quantity Ordered
- Unit Price
- Order Total (Calculated)
- Order Date
- Order Status

**Calculated Fields:**
- Order Total = Quantity × Unit Price (automated via trigger)

![Order Object Form](SCREENSHOTS/Handsmen%20Thread%20Order%20Creation.png)

---

## Automation & Business Logic

### Apex Triggers

#### 1. Order Calculation Trigger (`OrderTotalTrigger`)
**Purpose:** Automatically calculate order totals when orders are created or updated

**Trigger Events:**
- Before Insert
- Before Update

**Logic:**
- Retrieves product unit price
- Multiplies by quantity ordered
- Updates Order Total field

![Order Calculation Trigger](SCREENSHOTS/Order%20Calculation%20Trigger.png)

---

#### 2. Stock Deduction Trigger (`OrderTrigger`)
**Purpose:** Automatically deduct inventory when orders are placed

**Trigger Events:**
- After Insert
- After Update

**Logic:**
- Identifies products in the order
- Reduces inventory quantity
- Updates inventory records
- Calls handler class for processing

**Handler Class:** `OrderTriggerHandler`

![Stock Deduction Trigger](SCREENSHOTS/Stock%20Deduction%20Trigger.png)

---

### Batch Jobs

#### Inventory Monitoring Batch Job (`InventoryBatchJob`)
**Purpose:** Scheduled job to monitor inventory levels and trigger low stock alerts

**Schedule:** Daily execution (configurable)

**Process:**
1. Query all inventory records
2. Check current stock against reorder threshold
3. Identify products with low stock
4. Trigger low stock alert flow
5. Send notification emails

![Inventory Batch Job](SCREENSHOTS/InventoryBatchJob.png)

---

### Salesforce Flows

#### 1. Order Confirmation Flow
**Trigger:** When a new order is created

**Process:**
1. Retrieve order details
2. Get customer email
3. Populate email template
4. Send order confirmation email

![Order Confirmation Flow](SCREENSHOTS/Order%20Confirmation%20Flow.png)

---

#### 2. Low Stock Alert Flow
**Trigger:** When inventory falls below threshold or batch job detects low stock

**Process:**
1. Identify low stock products
2. Retrieve product details
3. Notify inventory manager
4. Send email alert with product information

![Low Stock Alert Flow](SCREENSHOTS/Low%20Stock%20Alert%20Flow.png)

---

#### 3. Loyalty Program Flow
**Trigger:** Based on customer purchase milestones

**Process:**
1. Track customer purchase history
2. Calculate loyalty points/status
3. Trigger reward notifications
4. Send loyalty program emails

![Loyalty Program Flow](SCREENSHOTS/Loyalty%20Program%20Flow.png)

---

## Email Notifications

### Email Template System

The application uses custom email templates for professional customer communications:

#### 1. Order Confirmation Email
**Purpose:** Confirm order placement to customers

**Content:**
- Order number and details
- Product information
- Quantity and pricing
- Expected delivery information
- Thank you message

![Order Confirmation Email](SCREENSHOTS/Order%20Confirmation%20Email.png)

---

#### 2. Low Stock Alert Email
**Purpose:** Notify inventory managers of low stock situations

**Content:**
- Product name and SKU
- Current stock level
- Reorder threshold
- Recommended action

![Low Stock Alert Email](SCREENSHOTS/Low%20Stock%20Alert%20Email.png)

![Low Stock Alert Email Template](SCREENSHOTS/Low%20Stock%20Alert%20Email%20Template.png)

---

#### 3. Loyalty Program Email
**Purpose:** Engage customers with loyalty rewards and promotions

**Content:**
- Customer name and loyalty status
- Available rewards
- Special offers
- Call to action

![Loyalty Program Email Template](SCREENSHOTS/Loyalty%20Program%20Email%20Template.png)

---

## Technical Implementation

### Data Validation

#### Email Validation
The system implements robust email validation to ensure data integrity:

**Validation Rules:**
- Proper email format (contains @ and domain)
- No duplicate emails in the system
- Required field enforcement

**Error Handling:**
- Clear error messages for users
- Prevents invalid data entry
- Provides guidance for correction

![Email Validation Error](SCREENSHOTS/Email%20Validation%20Error.png)

![Email Error](SCREENSHOTS/Email%20Error.png)

---

### Trigger Architecture

The application follows Salesforce best practices with a handler pattern:

**Design Pattern:**
```
Trigger → Handler Class → Business Logic
```

**Benefits:**
- Separation of concerns
- Reusable code
- Easier testing and maintenance
- Prevention of recursive triggers

---

### Batch Job Implementation

**Key Features:**
- Scheduled execution for automated monitoring
- Bulk processing for efficiency
- Error handling and logging
- Configurable thresholds

---

## User Interface

### Application Overview

The HandsMen Threads application provides a clean, intuitive interface for managing all aspects of the men's fashion e-commerce business.

![HandsMen Threads Application](SCREENSHOTS/Handsmen%20Threads%20Application.png)

### Key UI Features

1. **Navigation:** Easy access to all custom objects
2. **Forms:** Intuitive data entry screens
3. **Validation:** Real-time error messages
4. **Dashboard:** Overview of business metrics
5. **Responsive Design:** Works on desktop and mobile

---

## Testing & Validation

### Test Scenarios Covered

#### 1. Customer Creation
- ✅ Valid customer creation
- ✅ Email validation enforcement
- ✅ Duplicate email prevention
- ✅ Required field validation

#### 2. Order Processing
- ✅ Order total calculation accuracy
- ✅ Stock deduction verification
- ✅ Order confirmation email delivery
- ✅ Multiple order handling

#### 3. Inventory Management
- ✅ Real-time stock updates
- ✅ Low stock alert triggering
- ✅ Batch job execution
- ✅ Email notification delivery

#### 4. Email Communications
- ✅ Template rendering
- ✅ Dynamic data population
- ✅ Email delivery confirmation
- ✅ Professional formatting

---

## Technical Highlights

### Apex Code Components

1. **Triggers:**
   - `OrderTotalTrigger` - Order calculation automation
   - `OrderTrigger` - Stock deduction automation

2. **Handler Classes:**
   - `OrderTriggerHandler` - Order processing business logic

3. **Batch Jobs:**
   - `InventoryBatchJob` - Scheduled inventory monitoring

### Automation Flows

1. **Order Confirmation Flow** - Automated customer communications
2. **Low Stock Alert Flow** - Proactive inventory management
3. **Loyalty Program Flow** - Customer retention automation

### Custom Objects

1. **Customer** - Customer relationship management
2. **Product** - Catalog management
3. **Inventory** - Stock tracking
4. **Order** - Transaction processing

---

## Business Impact

### Operational Efficiency

- **Automated Calculations:** Eliminates manual order total calculations
- **Real-time Inventory:** Provides accurate stock information
- **Proactive Alerts:** Prevents stockouts with early warnings
- **Customer Communications:** Automated, professional email notifications

### Data Integrity

- **Validation Rules:** Ensures clean, accurate data
- **Error Prevention:** Catches issues before they enter the system
- **Audit Trail:** Tracks all changes and transactions

### Customer Experience

- **Quick Order Processing:** Streamlined ordering interface
- **Immediate Confirmation:** Instant order confirmation emails
- **Loyalty Recognition:** Automated loyalty program engagement

---

## Future Enhancements

### Phase 2 Features

1. **Shopping Cart Functionality**
   - Multi-product orders
   - Cart persistence
   - Discount code application

2. **Advanced Reporting**
   - Sales analytics dashboard
   - Inventory turnover reports
   - Customer purchase history

3. **Payment Integration**
   - Payment gateway integration
   - Multiple payment methods
   - Automated invoicing

4. **Enhanced Loyalty Program**
   - Points accumulation system
   - Tiered rewards structure
   - Referral program

5. **Mobile App**
   - Native mobile application
   - Push notifications
   - Mobile-optimized checkout

### Technical Improvements

1. **Test Coverage**
   - Expand Apex test classes
   - Achieve 100% code coverage
   - Automated testing pipeline

2. **Performance Optimization**
   - Query optimization
   - Bulk processing improvements
   - Caching strategies

3. **Integration Capabilities**
   - Third-party shipping APIs
   - External payment processors
   - Marketing automation platforms

---

## Conclusion

The HandsMen Threads capstone project successfully demonstrates a comprehensive Salesforce implementation for a men's fashion e-commerce platform. The application integrates custom objects, automation, business logic, and communications to create a complete business solution.

### Key Achievements

✅ **Custom Data Model** - Four custom objects working in harmony  
✅ **Automated Business Logic** - Triggers and handlers for calculations and updates  
✅ **Proactive Monitoring** - Batch jobs for inventory management  
✅ **Professional Communications** - Multiple email templates and flows  
✅ **Data Validation** - Robust error handling and validation rules  
✅ **User-Friendly Interface** - Intuitive screens for all operations  

### Learning Outcomes

This project provided hands-on experience with:
- Salesforce custom object development
- Apex programming (triggers, handlers, batch jobs)
- Salesforce Flow automation
- Email template creation
- Data validation and error handling
- Business process automation
- E-commerce system design

### Project Success Metrics

- ✅ All core features implemented and functional
- ✅ Automated processes working as designed
- ✅ Email notifications delivering successfully
- ✅ Data validation preventing errors
- ✅ Professional UI/UX implementation

---

## Appendices

### Appendix A: Screenshot Reference Guide

| Screenshot | Description | Section |
|------------|-------------|---------|
| `Handsmen Threads Application.png` | Main application interface | User Interface |
| `Create Account.png` | Customer account creation | Customer Management |
| `Email Validation Error.png` | Email validation error handling | Data Validation |
| `Email Error.png` | Email error message | Data Validation |
| `Handsmen Thread Customer Creation.png` | Customer creation form | Custom Objects |
| `Handsmen Thread Product Creation.png` | Product creation form | Custom Objects |
| `Handsmen Thread Inventory Creation.png` | Inventory creation form | Custom Objects |
| `Handsmen Thread Order Creation.png` | Order creation form | Custom Objects |
| `Order Calculation Trigger.png` | Order total calculation trigger | Apex Triggers |
| `Stock Deduction Trigger.png` | Inventory deduction trigger | Apex Triggers |
| `InventoryBatchJob.png` | Batch job configuration | Batch Jobs |
| `Order Confirmation Flow.png` | Order confirmation automation | Salesforce Flows |
| `Order Confirmation Email.png` | Order confirmation email | Email Notifications |
| `Low Stock Alert Flow.png` | Low stock alert automation | Salesforce Flows |
| `Low Stock Alert Email.png` | Low stock notification | Email Notifications |
| `Low Stock Alert Email Template.png` | Low stock email template | Email Notifications |
| `Loyalty Program Flow.png` | Loyalty program automation | Salesforce Flows |
| `Loyalty Program Email Template.png` | Loyalty program email | Email Notifications |

### Appendix B: Source Code Files

- `InventoryBatchJob.txt` - Inventory monitoring batch job
- `OrderTotalTrigger.txt` - Order calculation trigger
- `OrderTrigger.txt` - Stock deduction trigger
- `OrderTriggerHandler.txt` - Order processing handler

---

## Contact Information

**Student:** MJ Tuplano  
**Project:** HandsMen Threads Capstone  
**Platform:** Salesforce  
**Submission Date:** November 28, 2025

---

*This documentation represents the complete implementation of the HandsMen Threads e-commerce platform built on Salesforce, demonstrating proficiency in custom development, automation, and business process implementation.*
