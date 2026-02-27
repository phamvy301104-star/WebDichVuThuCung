# Test Cases - Authentication Module

| # | Test Case | Input | Expected | Result |
|---|-----------|-------|----------|--------|
| 1 | Dang ky email hop le | email, password, fullName | 201 Created + JWT | PASS |
| 2 | Dang ky email da ton tai | existing email | 400 Error | PASS |
| 3 | Dang ky thieu field | missing password | 400 Validation Error | PASS |
| 4 | Dang nhap dung | email + password | 200 + access_token + refresh_token | PASS |
| 5 | Dang nhap sai password | email + wrong pass | 401 Unauthorized | PASS |
| 6 | Dang nhap email khong ton tai | fake email | 401 Unauthorized | PASS |
| 7 | Refresh token hop le | valid refresh_token | 200 + new access_token | PASS |
| 8 | Refresh token het han | expired token | 401 Token expired | PASS |
| 9 | Access protected route no token | No auth header | 401 Unauthorized | PASS |
| 10 | Access admin route as customer | Customer token | 403 Forbidden | PASS |
| 11 | Google OAuth login | Google account | 200 + JWT | PASS |
| 12 | Upload avatar | Image file | 200 + avatar URL | PASS |
| 13 | Update profile | fullName, phone | 200 Updated profile | PASS |
| 14 | CRUD Product (Admin) | Product data | 201/200/200/200 | PASS |
| 15 | Filter products by category | category_id | Filtered products list | PASS |
| 16 | Search products by name | search keyword | Matching products | PASS |
