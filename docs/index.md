# ExpenseEase — Expense Tracker App

**ExpenseEase** is a cross-platform mobile application that helps individuals manage their personal finances by tracking income and expenses.  
It provides an ad-free and fully accessible experience, solving the issue of in-app purchase restrictions present in many other expense tracking apps.

# Introduction
ExpenseEase is a mobile application developed using Flutter with a Node.js and Express backend, connected to a PostgreSQL database(AWS RDS).  
It enables users to track income and expenses, view total balance.

The app includes authentication through JWT and supports two roles: **User** and **Admin**.  
Admins can view registered users, while individual users manage their own transactions.

# Scope and Objectives
## Scope
ExpenseEase provides users with a simple, free, and secure platform to manage daily financial activities.  
It includes secure login, transaction tracking, dashboard summaries, and analytics.

## Objectives
- Allow users to record income and expenses.
- Display real-time balance and recent transactions.
- Enable CRUD operations on financial entries.
- Support admin access to view registered users.
