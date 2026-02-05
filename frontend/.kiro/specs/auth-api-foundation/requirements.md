# Requirements Document

## Introduction

The Auth & API Foundation feature establishes the core authentication, authorization, and API communication infrastructure for the ShopBike frontend application. This foundation enables secure user authentication with role-based access control, protected routing, and a robust API layer with token management and refresh capabilities.

## Glossary

- **System**: The ShopBike frontend application
- **Auth_Store**: Zustand store managing authentication state with persistence
- **API_Client**: Centralized Axios instance for HTTP communication
- **Router**: React Router v6 browser router with protected routes
- **Guard**: Route protection component that enforces authentication/authorization
- **Token**: JWT access token for API authentication
- **Refresh_Token**: Long-lived token for obtaining new access tokens
- **Role**: User permission level (BUYER, SELLER, INSPECTOR, ADMIN)
- **Form_Schema**: Zod validation schema for form inputs
- **Service_Layer**: API abstraction layer between components and HTTP client

## Requirements

### Requirement 1: Enhanced Authentication Store

**User Story:** As a developer, I want a persistent authentication store with comprehensive token management, so that user sessions are maintained across browser refreshes and provide role-based access control.

#### Acceptance Criteria

1. THE Auth_Store SHALL persist authentication state using the key "auth-storage"
2. WHEN tokens are set, THE Auth_Store SHALL store accessToken, refreshToken, and role
3. WHEN tokens are cleared, THE Auth_Store SHALL reset all authentication state to null
4. THE Auth_Store SHALL support four roles: BUYER, SELLER, INSPECTOR, and ADMIN
5. THE Auth_Store SHALL provide setTokens and clearTokens actions for state management

### Requirement 2: Modern Router Architecture

**User Story:** As a developer, I want a modern router structure using createBrowserRouter, so that the application has better performance and follows React Router v6 best practices.

#### Acceptance Criteria

1. THE Router SHALL use createBrowserRouter instead of BrowserRouter
2. THE Router SHALL implement MainLayout with Outlet for nested routing
3. WHEN routes are defined, THE Router SHALL organize them hierarchically under layouts
4. THE Router SHALL support both public and protected route configurations
5. THE Router SHALL keep existing public route paths unchanged (e.g., /, /login, /bikes/:id, …)

### Requirement 3: Comprehensive Route Guards

**User Story:** As a user, I want secure route protection that redirects me appropriately based on my authentication status, so that I can access only the pages I'm authorized to view.

#### Acceptance Criteria

1. WHEN an unauthenticated user accesses a protected route, THE RequireAuth guard SHALL redirect to /login with location state
2. WHEN an authenticated user accesses /login, THE GuestGuard SHALL redirect to the original destination or home
3. THE RequireAuth guard SHALL preserve the attempted route in location state for post-login redirect
4. THE GuestGuard SHALL check for existing accessToken before allowing access to login page
5. WHEN redirecting after login, THE System SHALL navigate to the preserved location or default route

### Requirement 4: Role-Based Registration and Login

**User Story:** As a user, I want to register and login with appropriate role restrictions, so that I can access the system with the correct permissions for my account type.

#### Acceptance Criteria

1. THE Login_Form SHALL support selection of all four roles: BUYER, SELLER, INSPECTOR, ADMIN
2. THE Register_Form SHALL restrict role selection to only BUYER and SELLER
3. WHEN a user registers, THE System SHALL prevent selection of INSPECTOR or ADMIN roles
4. THE Login_Form SHALL validate credentials using Zod schema validation
5. THE Register_Form SHALL validate user input using Zod schema validation
6. WHEN form validation fails, THE System SHALL display field-specific error messages
7. THE System SHALL treat role as an account attribute; a user cannot log in as a different role than their account’s role

### Requirement 5: Schema-First Form Validation

**User Story:** As a developer, I want centralized form validation schemas, so that validation logic is consistent and maintainable across the application.

#### Acceptance Criteria

1. THE System SHALL store all validation schemas in src/utils/rules.ts
2. THE Login_Form SHALL use React Hook Form with zodResolver for validation
3. THE Register_Form SHALL use React Hook Form with zodResolver for validation
4. WHEN forms are submitted, THE System SHALL prevent submission during validation or API calls
5. THE System SHALL map backend 422 errors to specific form fields using setError

### Requirement 6: Robust API Client with Token Management

**User Story:** As a developer, I want a centralized API client with automatic token attachment and refresh handling, so that API communication is secure and resilient.

#### Acceptance Criteria

1. THE API_Client SHALL automatically attach JWT tokens to all requests via interceptors
2. WHEN a 401 response is received, THE API_Client SHALL attempt token refresh once using _retry flag
3. WHEN token refresh fails, THE API_Client SHALL clear tokens and redirect to login
4. THE API_Client SHALL normalize responses by returning response.data to components
5. THE API_Client SHALL use a separate axios instance for refresh requests to avoid interceptor loops
6. THE Service_Layer SHALL provide normalized API methods that components call instead of axios directly
7. THE API_Client SHALL prevent multiple simultaneous refresh calls by queueing pending requests while refreshing

### Requirement 7: Component API Abstraction

**User Story:** As a developer, I want components to interact with APIs through service layer methods, so that API logic is centralized and components remain clean.

#### Acceptance Criteria

1. THE System SHALL provide service layer APIs (authApi, userApi) for component consumption
2. WHEN components need API data, THE System SHALL prevent direct axios calls from components
3. THE Service_Layer SHALL handle API response normalization and error formatting
4. THE Service_Layer SHALL provide consistent method signatures across different API endpoints
5. THE Service_Layer SHALL integrate with the centralized API_Client for all HTTP communication

### Requirement 8: Profile Test Page Implementation

**User Story:** As a developer, I want a test page that demonstrates authentication, guards, and API behavior, so that I can verify the foundation works correctly.

#### Acceptance Criteria

1. THE Profile_Test_Page SHALL display current user authentication state and role
2. WHEN loading user data, THE Profile_Test_Page SHALL show Loading state
3. WHEN API errors occur, THE Profile_Test_Page SHALL show Error state with retry option
4. WHEN no user data exists, THE Profile_Test_Page SHALL show Empty state with appropriate message
5. THE Profile_Test_Page SHALL demonstrate token refresh behavior when tokens expire
6. THE Profile_Test_Page SHALL provide logout functionality that clears tokens and redirects

### Requirement 9: shadcn/ui Integration

**User Story:** As a developer, I want forms and UI components to use shadcn/ui components, so that the interface is consistent and follows design system standards.

#### Acceptance Criteria

1. THE Login_Form SHALL use shadcn/ui Button, Input, and Form components
2. THE Register_Form SHALL use shadcn/ui Button, Input, and Form components
3. THE Profile_Test_Page SHALL use shadcn/ui Card, Button, and Badge components for state display
4. WHEN forms show validation errors, THE System SHALL use shadcn/ui error styling
5. THE System SHALL maintain consistent component styling across all authentication flows
