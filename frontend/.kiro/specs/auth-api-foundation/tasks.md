# Implementation Plan: Auth & API Foundation

## Overview

This implementation plan establishes the core authentication and API infrastructure for ShopBike frontend using React Router v6 createBrowserRouter, enhanced Zustand auth store, robust API client with token refresh, and shadcn/ui forms with React Hook Form + Zod validation. The implementation follows a progressive approach, building from core infrastructure to user-facing features.

## Tasks

- [ ] 1. Set up enhanced authentication store and validation schemas
  - Update Zustand auth store to support four roles (BUYER, SELLER, INSPECTOR, ADMIN)
  - Create src/utils/rules.ts with Zod schemas for login and registration forms
  - Implement persistent storage with auth-storage key
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 5.1_

- [ ] 1.1 Write property tests for auth store
  - **Property 1: Auth Store State Management**
  - **Property 2: Auth Store State Reset**
  - **Property 3: Role Validation**
  - **Validates: Requirements 1.1, 1.2, 1.3, 1.4**

- [ ] 2. Implement modern router architecture with createBrowserRouter
  - [ ] 2.1 Create new router configuration using createBrowserRouter
    - Replace BrowserRouter with createBrowserRouter in AppRouter.tsx
    - Implement nested route structure with MainLayout and Outlet
    - Configure full-screen auth pages outside MainLayout
    - _Requirements: 2.1, 2.2, 2.3_

  - [ ] 2.2 Update route guards for enhanced functionality
    - Enhance RequireAuth guard with location state preservation
    - Update GuestGuard with proper redirect logic for authenticated users
    - Create RequireRole guard for role-based access control
    - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5_

  - [ ] 2.3 Write property tests for route guards
    - **Property 4: Route Protection**
    - **Property 5: Guest Guard Redirection**
    - **Validates: Requirements 3.1, 3.2, 3.3, 3.5**

- [ ] 3. Build robust API client with token refresh and concurrency control
  - [ ] 3.1 Implement enhanced API client with interceptors
    - Create centralized logout handler with React Router navigation fallback
    - Implement request interceptor for automatic token attachment
    - Build response interceptor with concurrency-safe token refresh
    - Add refresh concurrency control (isRefreshing flag, refreshPromise, subscriber queue)
    - _Requirements: 6.1, 6.2, 6.3, 6.4, 6.5_

  - [ ] 3.2 Create service layer APIs
    - Implement authApi with login, register, logout, getCurrentUser, refreshToken methods
    - Implement userApi with getProfile and updateProfile methods
    - Ensure all endpoints use /api prefix following backend Swagger specification
    - _Requirements: 7.1, 7.3, 7.4, 7.5_

  - [ ] 3.3 Write property tests for API client
    - **Property 8: API Token Attachment**
    - **Property 9: Token Refresh on 401**
    - **Property 10: Refresh Failure Handling**
    - **Property 11: Refresh Concurrency Control**
    - **Property 12: Response Normalization**
    - **Validates: Requirements 6.1, 6.2, 6.3, 6.4, 6.6**

- [ ] 4. Checkpoint - Verify core infrastructure
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 5. Create authentication forms with shadcn/ui and React Hook Form
  - [ ] 5.1 Build login page with role selection
    - Create LoginPage component using shadcn/ui Form, Input, Button components
    - Implement React Hook Form with zodResolver and loginSchema
    - Add role selector supporting all four roles (BUYER, SELLER, INSPECTOR, ADMIN)
    - Handle form submission with proper error mapping and loading states
    - _Requirements: 4.1, 4.4, 5.2, 5.4, 5.5, 9.1_

  - [ ] 5.2 Build registration page with role restrictions
    - Create RegisterPage component using shadcn/ui Form, Input, Button components
    - Implement React Hook Form with zodResolver and registerSchema
    - Restrict role selection to only BUYER and SELLER
    - Add password confirmation validation and terms acceptance
    - _Requirements: 4.2, 4.3, 4.5, 5.3, 5.4, 5.5, 9.2_

  - [ ] 5.3 Write property tests for form validation
    - **Property 6: Registration Role Restriction**
    - **Property 7: Form Validation Behavior**
    - **Property 15: Form Error Styling**
    - **Validates: Requirements 4.2, 4.3, 4.4, 4.5, 4.6, 5.4, 9.4, 9.5**

- [ ] 6. Implement profile test page for verification
  - [ ] 6.1 Create ProfileTestPage component
    - Build page using shadcn/ui Card, Button, Badge components
    - Implement Loading, Error, Empty, and Success states
    - Display current authentication state and user role information
    - Add logout functionality with proper token clearing and navigation
    - _Requirements: 8.1, 8.2, 8.3, 8.4, 8.6, 9.3_

  - [ ] 6.2 Add token refresh demonstration
    - Implement functionality to test token refresh behavior
    - Show token expiration handling and automatic refresh
    - Provide manual refresh trigger for testing
    - _Requirements: 8.5_

  - [ ] 6.3 Write property tests for profile page
    - **Property 13: Profile Page State Management**
    - **Property 14: Logout Behavior**
    - **Validates: Requirements 8.1, 8.2, 8.3, 8.4, 8.6**

- [ ] 7. Integration and wiring
  - [ ] 7.1 Wire authentication forms to auth store and API
    - Connect login form to authApi.login and auth store setTokens
    - Connect register form to authApi.register and auth store setTokens
    - Implement post-authentication navigation with preserved routes
    - _Requirements: 4.4, 4.5, 7.1_

  - [ ] 7.2 Update existing components to use new router structure
    - Update MainLayout to work with Outlet pattern
    - Ensure existing route guards work with new router configuration
    - Test navigation flows between authenticated and unauthenticated states
    - _Requirements: 2.4, 2.5_

  - [ ] 7.3 Write integration tests
    - Test complete authentication flow from login to protected routes
    - Test token refresh during active user sessions
    - Test role-based access control across different user types
    - _Requirements: 3.1, 3.2, 3.5, 4.1, 4.2_

- [ ] 8. Final checkpoint - Comprehensive testing
  - Ensure all tests pass, ask the user if questions arise.

## Notes

- Each task references specific requirements for traceability
- Checkpoints ensure incremental validation of core functionality
- Property tests validate universal correctness properties using fast-check library
- Unit tests validate specific examples, edge cases, and integration points
- All forms use shadcn/ui components with React Hook Form and Zod validation
- API endpoints follow backend Swagger specification with /api prefix
- Authentication pages render outside MainLayout for full-screen experience